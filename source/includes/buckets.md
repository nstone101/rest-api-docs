# Buckets


## Add Bucket
`title` is the only required property.  See the table below for the other optional properties.  The Bucket request matches the `bucket.json` file located in Your Bucket Dashboard > Import Export.


> Definition

```bash
POST https://api.cosmicjs.com/v1/buckets
```

```javascript
Cosmic.addBucket()
```

> Example Request

```bash
curl -X POST https://api.cosmicjs.com/v1/buckets \
-H "Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXV.eyJlbWFpbCI6InNwaXJvbnlAZ21haWwuY29tIiwicGFzc3dvcmQiOiIxNzlhZDQ1YzZjZTJjYjk3Y2YxMDI5ZTIxMjA0NmU4MSIsImlhdCI6MTUxNDQ5NzI3N30.ep4cEgH_SqItQ5McJArJtljS3GSJedyEcDRlnu9yb-U" \
-H "Content-Type: application/json" \
-d '{"title": "My New Bucket"}'
```

```javascript
const Cosmic = require('cosmicjs')({
  token: 'your-token-from-auth-request' // from Cosmic.authenticate
})
Cosmic.addBucket({
  title: 'My New Bucket',
  slug: 'my-new-bucket' // must be unique across all Buckets in system
}).then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

> Example Response

```json
{
  "bucket": {
    "_id": "55b3d557df0fb1df7600004b",
    "slug": "my-new-bucket",
    "title": "My New Bucket"
  }
}
```

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
title | required | String | Your Bucket title
slug |  | String | URL-friendly unique identifier
read_key |  | String | Restrict read access
write_key |  | String | Restrict write access
cluster |  | String | Add this Bucket to a Cluster.  ID of existing Cluster
object_types |  | Array | Populate your Bucket with Object Types.  See <a href="#object-types">Object Types</a> for model.
objects |  | Array | Populate your Bucket with Objects. See <a href="#objects">Objects</a> for model.
media |  | Array | Populate your Bucket with Media. See <a href="#media">Media</a> for model.
media_folders |  | Array | Populate your Bucket with Media Folders. See <a href="#media">Media</a> for model.
webhooks |  | Array | Populate your Bucket with <a href="https://cosmicjs.com/docs/webhooks" target="_blank">Webhooks</a>. See <a href="#webhooks">Webhooks</a> for model.
extensions |  | Array | Populate your Bucket with <a href="https://cosmicjs.com/docs/extensions" target="_blank">Extensions</a>. See <a href="#extensions">Extensions</a> for model.

## Connect to Bucket

> Example Request

```bash
GET https://api.cosmicjs.com/:bucket_slug
```

```javascript
// Use the Cosmic.bucket method to connect to different Buckets in your account.
const Cosmic = require('cosmicjs')({
  token: 'your-token-from-auth-request' // from Cosmic.authenticate
})
const bucket1 = Cosmic.bucket({
  bucket: 'my-first-bucket',
  read_key: '',
  write_key: ''
})
const bucket2 = Cosmic.bucket({
  bucket: 'my-other-bucket',
  read_key: '',
  write_key: ''
})
```

For the NPM module:

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
bucket |  | String | The Bucket slug
read_key |  | String | Restrict read access
write_key |  | String | Restrict write access

## Get Bucket

> Definition

```bash
GET https://api.cosmicjs.com/:bucket_slug
```

```javascript
bucket.getBucket()
```

> Example Request

```bash
curl "https://api.cosmicjs.com/v1/wedding-site"
```

```javascript
const Cosmic = require('cosmicjs')({
  token: 'your-token-from-auth-request' // from Cosmic.authenticate
})
const bucket = Cosmic.bucket({
  bucket: 'wedding-site',
  read_key: ''
})
bucket.getBucket().then(data => {
  console.log(data)
}).catch(err => {
  console.log(err)
})
```

> Example Response

```json
{
  "bucket": {
    "_id": "55b3d557df0fb1df7600004b",
    "slug": "wedding-site",
    "title": "Wedding Site",
    "object_types": [
      ...
    ],
    "objects": [
      ...
    ],
    "media": [
      ...
    ],
    "media_folders": [
      ...
    ]
  }
}
```


Returns the entire Bucket including Object Types, Objects, Media and more.  If you would like to restrict read access to your Bucket, you can do so in Your Bucket > Basic Settings.

Parameter | Required | Type | Description
--------- | ------- | ----------- | -----------
hide_metafields |  | Enum | true, Hides metafields
read_key |  | String | Restrict read access to your Bucket