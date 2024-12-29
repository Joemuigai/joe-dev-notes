<!-- Laravel s3 notes -->

# Laravel S3 Notes

## Driver Prerequisites

1. Install the Flysystem S3 package using Composer:

```bash
composer require league/flysystem-aws-s3-v3 "^3.0" --with-all-dependencies
```

2. Add the following environment variables to your `.env` file:

```bash
AWS_ACCESS_KEY_ID=<your-key-id>
AWS_SECRET_ACCESS_KEY=<your-secret-access-key>
AWS_DEFAULT_REGION=us-east-1
AWS_BUCKET=<your-bucket-name>
AWS_USE_PATH_STYLE_ENDPOINT=false
```

3. Add the following disk to your `config/filesystems.php` file:

```php
's3' => [
    'driver' => 's3',
    'key' => env('AWS_ACCESS_KEY_ID'), // AWS_ACCESS_KEY_ID environment variable in .env file 
]
```

4. Use the `Storage` facade to interact with the S3 disk:

```php
use Illuminate\Support\Facades\Storage; // Import the Storage facade at the top of your file 
```

## Usage

### Storing Files

```php
Storage::disk('s3')->put('file.jpg', $fileContents); // Store a file on S3
```

### Retrieving Files

```php
$contents = Storage::disk('s3')->get('file.jpg'); // Retrieve a file from S3
```

### Deleting Files

```php
Storage::disk('s3')->delete('file.jpg'); // Delete a file from S3
```

### Checking if a File Exists

```php
$exists = Storage::disk('s3')->exists('file.jpg'); // Check if a file exists on S3
```

### Getting the URL of a File

```php
$url = Storage::disk('s3')->url('file.jpg'); // Get the URL of a file on S3
```

### Directories

```php
Storage::disk('s3')->makeDirectory('path/to/directory'); // Create a directory on S3
Storage::disk('s3')->deleteDirectory('path/to/directory'); // Delete a directory on S3
```

### Visibility

```php
Storage::disk('s3')->setVisibility('file.jpg', 'public'); // Set the visibility of a file on S3
```

### File Metadata

```php
$size = Storage::disk('s3')->size('file.jpg'); // Get the size of a file on S3
$lastModified = Storage::disk('s3')->lastModified('file.jpg'); // Get the last modified timestamp of a file on S3
```

### File Streams

```php
$stream = Storage::disk('s3')->readStream('file.jpg'); // Get a read stream for a file on S3
Storage::disk('s3')->writeStream('file.jpg', $stream); // Write a stream to a file on S3
```

### Temporary URLs

```php
$url = Storage::disk('s3')->temporaryUrl('file.jpg', now()->addMinutes(5)); // Get a temporary URL for a file on S3
```

### Custom Endpoints

```php
Storage::disk('s3')->getAdapter()->getClient()->setEndpoint('https://custom-endpoint.com'); // Set a custom endpoint for S3
```

### Custom Headers

```php
Storage::disk('s3')->getAdapter()->getClient()->putObject([ // Set custom headers for a file on S3
    'Bucket' => 'your-bucket-name',
    'Key' => 'file.jpg',
    'Body' => $fileContents,
    'ContentType' => 'image/jpeg',
    'ACL' => 'public-read',
]);
```

### Multipart Uploads

```php
$uploader = new MultipartUploader(Storage::disk('s3')->getAdapter()->getClient(), $fileContents, [ // Perform a multipart upload to S3
    'bucket' => 'your-bucket-name',
    'key' => 'file.jpg',
]);

try {
    $result = $uploader->upload();
} catch (MultipartUploadException $e) {
    $uploader->abort();
}
```

### Presigned URLs

```php
$command = $s3Client->getCommand('GetObject', [ // Generate a presigned URL for a file on S3
    'Bucket' => 'your-bucket-name',
    'Key' => 'file.jpg',
]);

$request = $s3Client->createPresignedRequest($command, '+20 minutes');

$presignedUrl = (string) $request->getUri();
```

### Custom Configuration

```php
$adapter = new AwsS3Adapter(Storage::disk('s3')->getAdapter()->getClient(), 'your
-bucket-name', 'optional-prefix'); // Create a custom adapter for S3

$filesystem = new Filesystem($adapter);

Storage::extend('custom-s3', function ($app, $config) use ($filesystem) { // Extend the Storage facade with a custom S3 disk
    return $filesystem;
});

Storage::disk('custom-s3')->put('file.jpg', $fileContents); // Use the custom S3 disk
```

## References

- [AWS SDK for PHP Documentation](https://docs.aws.amazon.com/sdk-for-php/index.html)
- [Laravel Storage Documentation](https://laravel.com/docs/8.x/filesystem)
- [Laravel Filesystem Documentation](https://laravel.com/docs/8.x/filesystem)