---
title: "Upload files to MongoDB GridFS with Express"
date: 2020-09-21T12:00:02+05:30
tags: ["Express", "MongoDB", "GridFS", "Multer", 'JavaScript', 'NodeJS', 'Database', 'Mongoose']
---

Create express based APIs to upload and download files to and from MongoDB GridFS.

> [GridFS](https://docs.mongodb.com/manual/reference/glossary/#term-gridfs) is a specification for storing and retrieving files that exceed the BSON-document size limit of 16 MB.

# Install Dependencies
- `express` to create the APIs
- `multer` to handle multi-part file uploads
- `mongoose` to manage connections to MongoDB
- `gridfile` to manage interactions with GridFS

# GridFile Mongoose Model
[GridFile](https://github.com/abskmj/gridfile) is a reusable Mongoose Schema for MongoDB GridFS.

```javascript
// gridfile.model.js

const mongoose = require('mongoose')
const schema = require('gridfile')

module.exports = mongoose.model('GridFile', schema)
```

# Multer Middleware
[Multer](https://www.npmjs.com/package/multer) will parse `multipart/form-data` request and the uploaded files will be accessible as `req.files`

```javascript
const multer = require('multer')
const upload = multer({ dest: path.join(__dirname, '.') })
```

# Upload File API
API uses the multer middleware and GridFile model to upload files to GridFS.

```javascript
app.post('/v1/files', upload.any(), async (req, res, nxt) => {
  try {
    // uploaded file are accessible as req.files
    if (req.files) {
      const promises = req.files.map(async (file) => {
        const fileStream = fs.createReadStream(file.path)

        // upload file to gridfs
        const gridFile = new GridFile({ filename: file.originalname })
        await gridFile.upload(fileStream)

        // delete the file from local folder
        fs.unlinkSync(file.path)
      })

      await Promise.all(promises)
    }

    res.sendStatus(201)
  } catch (err) {
    nxt(err)
  }
})
```

# List Files API
API returns information about uploaded files.

```javascript
app.get('/v1/files', async (req, res, nxt) => {
  try {
    const files = await GridFile.find({})

    res.json(files)
  } catch (err) {
    nxt(err)
  }
})
```

Sample response

```json
[
  {
    "aliases": [],
    "_id": "5f6850023516552ad21d0007",
    "length": 7945,
    "chunkSize": 261120,
    "uploadDate": "2020-09-21T07:02:26.389Z",
    "filename": "attachment.pdf",
    "md5": "fa7d7e650b2cec68f302b31ba28235d8"
  }
]
```

# Download File API
API returns the file from the GridFS using its id.

```javascript
app.get('/v1/files/:id/:name', async (req, res, nxt) => {
  try {
    const { id, name } = req.params

    const gridFile = await GridFile.findById(id)

    if (gridFile) {
      res.attachment(name)
      gridFile.downloadStream(res)
    } else {
      // file not found
      res.status(404).json({ error: 'file not found' })
    }
  } catch (err) {
    nxt(err)
  }
})
```

Sample Request URL
```
/v1/files/5f6850023516552ad21d0007/attachment.pdf
```

> A working codebase for reference is available at [gist.github.com](https://gist.github.com/abskmj/655dbc3191e108d6a5a55e28446bc1e9)