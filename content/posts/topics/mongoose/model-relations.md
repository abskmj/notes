---
title: "Model Relations in Mongoose"
date: 2018-12-24T09:35:35Z
tags: ["Topic","Mongoose","Model","Relations"]
---

# Model Relations

Relations are logical links which define how models are connected with each other. A document of a model can be connected to one or more documents of same or another model.

A relation between models are generally of two types:

- **BelongsTo**: A document in source model is connected with a document in destination model by putting the id of destination document in the source document.
- **Has Many / Has One**: A document in source model is connected with one or many documents in destination models by putting the id of the source document in destination document(s).


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
Post.find({}).populate('author');
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
});
```

## Populate
Now the author of a blog post can be easily populated by:
```javascript
Post.find({}).populate('posts');
```

# Code Repository
A working code respository is available at [github](https://github.com/abskmj/example-model-relations).