---
title: "Model Relations in Mongoose"
date: 2018-12-24T09:35:35Z
tags: ["Topic","Mongoose","Model","Relations"]
---

# Model Relations

Relations are logical links which define how models are connected with each other. A document of a model can be connected to one or more documents of the same or another model.

A relation between models are generally of two types:

- **Belongs To**: A document in the source model is connected with a document in the destination model by putting the id of the destination document in the source document.
- **Has Many / Has One**: A document in the source model is connected with one or many documents in destination models by putting the id of the source document in destination document(s).


# Relation: Belongs To

## Example
> A blog post belongs to a user

### User Schema
```javascript
{
    name: {
        type: String,
        required: true
    }
}
```

### Blog Post Schema
```javascript
{
    name: {
        type: String,
        required: true
    },
    author: {
        type: Schema.Types.ObjectId,
        ref: 'User',
        required: true
    }
}
```

## Populate
Now the author of a blog post can be easily populated by:
```javascript
Post.find({}).populate('author')

/*
  {
    _id: 5f71af94e66f4728f68ffc06,
    name: 'Relation: Belongs To',
    author: {
      _id: 5f71af94e66f4728f68ffc05,
      name: 'abskmj',
      email: 'abskmj@email.com'
    }
  }
*/
```

# Relation: Has Many / Has One

## Example
> A user has many blog posts

### User Schema
```javascript
schema.virtual('posts', {
    ref: 'Post',
    localField: '_id',
    foreignField: 'author'
})
```

## Populate
Now the author of a blog post can be easily populated by:
```javascript
User.find({}).populate('posts')

/*
  {
    _id: 5f71ce43687f2a2fb97fa462,
    name: 'abskmj',
    email: 'abskmj@email.com',
    posts: [
      {
        _id: 5f71ce43687f2a2fb97fa463,
        name: 'Relation: Belongs To',
        author: 5f71ce43687f2a2fb97fa462
      },
      {
        _id: 5f71ce43687f2a2fb97fa464,
        name: 'Relation: Has One',
        author: 5f71ce43687f2a2fb97fa462
      }
    ],
    id: '5f71ce43687f2a2fb97fa462'
  }
*/
```

# Note 
Virtuals are not included in string version of the model instances by default. To include them, set the `virtuals` option to `true` on schema's `toObject` and `toJSON` options.
``` javascript
const User = new Schema(userSchema, {
    toObject: { virtuals: true }, 
    toJSON: { virtuals: true } 
})
```


> A working codebase for reference is available at [gist.github.com](https://gist.github.com/abskmj/cb5bb57829c677fe38b724ad864eaa5b)

# Reference
- Populate Virtuals at [mongoosejs.com](https://mongoosejs.com/docs/populate.html#populate-virtuals)