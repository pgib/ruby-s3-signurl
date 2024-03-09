# Signing an S3 URL

## Y tho?

There are cases where I want to send a file to someone, but I either don't want the attachment to live in their email inbox or message history, or maybe the file is too large to practically send that way. So I opt to use an S3 bucket to house the file.

But I also don't want a public bucket nor do I want the link to the file to persist forever. Enter an expiring, presigned URL--courtesy of AWS S3.

## Usage

1. Run `bundle` to install required gems.

2. Copy the `.env.sample` to `.env` and configure as necessary. If you set `S3_BUCKET`, you can provide just the key you wish to sign. You will need to set `AWS_REGION` to the region your bucket resides if you do not already have this set in your environment.

Run:

```sh
./signurl s3://<bucket>/<key>
```

or if you have `S3_BUCKET` set in the `.env` file:

```sh
./signurl <key>
```

By default, the link will expiry in 86,400 seconds (24 hours); however, you can override this by setting `S3_URL_EXPIRY` to the number of seconds you want your link to last. Note that this may also be subject to the _maximum session duration_ if your credentials come from assuming a role: it will be the lesser of the two no matter what you set.
