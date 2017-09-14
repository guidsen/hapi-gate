# Hapi Gate - Draft Proposal
A authorization plugin that works seamlessly with any NodeJS web framework. Inspired by [Laravel](https://laravel.com).

## Components

- [ ] The Gate
- [ ] Policies
- [ ] Abilities

## Usage

```javascript
const { Gate, Policy } = require('hapi-gate);

const abilities = {
  create(post, user) {
    return user.role === 'admin';
  },
  update(post, user) {
    return post.userId === user.id;
  },
};

const PostPolicy = new Policy('post', abilities);
const Gate = new Gate({
  policies: [PostPolicy],
  resolveUser: (req) => {
    // This will be passed to the policies
    return req.auth.credentials;
  },
});

if (Gate.allows(create-post, post)) {
  // User is allowed to create the post
}

// Using `authorize`, an error will be thrown when the user is not authorized.
Gate.authorize('create-post', post);
```

