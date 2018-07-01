# Comments

[![Latest Stable Version](https://poser.pugx.org/laravelista/comments/v/stable)](https://packagist.org/packages/laravelista/comments)
[![Total Downloads](https://poser.pugx.org/laravelista/comments/downloads)](https://packagist.org/packages/laravelista/comments)
[![License](https://poser.pugx.org/laravelista/comments/license)](https://packagist.org/packages/laravelista/comments)

[![forthebadge](http://forthebadge.com/images/badges/built-with-love.svg)](http://forthebadge.com)

Comments is a Laravel package. With it you can easily implement native comments for your application.

## Overview

This package can be used to comment on any model you have in your application.

All comments are stored in a single table with a polymorphic relation for content and a one-to-many relation for the user who posted the comment.

### Todo

- [x] Create comment
- [x] Delete comment
- [x] Edit Comment
- [x] Reply to comment
- [ ] Send Events

### Screenshots

Here are a few screenshots.

No comments & guest:

__New screenshots coming soon.__

No comments & logged in:

__New screenshots coming soon.__

One comment:

__New screenshots coming soon.__

One comment edit form:

__New screenshots coming soon.__

Two comments from different users:

__New screenshots coming soon.__

### Tutorials & articles

I plan to expand this chapter with more tutorials and articles. If you write something about this package let me know, so that I can update this chapter.

**Articles:**

- [Laravelista: Comments preview (Outdated)](https://laravelista.com/posts/comments-preview)

## Installation

From the command line:

```bash
composer require laravelista/comments
```

### Run migrations

We need to create the table for comments.

```bash
php artisan migrate
```

### Add Commenter trait to your User model

Add the `Commenter` trait to your User model so that you can retrieve the comments for a user:

```php
use Laravelista\Comments\Commenter;

class User extends Authenticatable
{
    use Notifiable, Commenter;
}
```

### Add Commentable trait to models

Add the `Commentable` trait to the model for which you want to enable comments for:

```php
use Laravelista\Comments\Commentable;

class Product extends Model
{
    use Commentable;
}
```

### Publish Config & configure (optional)

In the `config` file you can specify:

- where is your User model located; the default is `\App\User::class`

Publish the config file (optional):

```bash
php artisan vendor:publish --provider="Laravelista\Comments\ServiceProvider" --tag=config
```

### Publish views (customization)

The default UI is made for Bootstrap 4, but you can change it however you want.

```bash
php artisan vendor:publish --provider="Laravelista\Comments\ServiceProvider" --tag=views
```

## Usage

In the view where you want to display comments, place this code and modify it:

```
@comments(['model' => $book])
@endcomments
```

In the example above we are setting the `commentable_type` to the class of the model. We are also passing the `commentable_id` the `id` of the book so that we know to which book the comments relate to. Behind the scenes, the package detects the currently logged in user if any.

If you open the page containing the view where you have placed the above code, you should see a working comments form.
