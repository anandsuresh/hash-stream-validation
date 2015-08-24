# hash-stream-validation
> Hash a stream of data, then validate

```sh
$ npm install --save hash-stream-validation
```
```js
var hashStreamValidation = require('hash-stream-validation');

var validateStream = hashStreamValidation();

fs.createReadStream(filePath)
  .pipe(validate)
  .on('data', function() { /*... */ })
  .on('end', function() {
    validate.test('md5', /*checksum*/);
  });
```

## Use Case

After a successful upload to a Google Cloud Storage bucket, the API will respond with the hash of data it has received. During our upload, we can run the data through this module, then confirm after the upload if we both arrived at the same results. If not, we know something went wrong during the transmission.

## API

### validateStream = hashStreamValidation([opts])

#### opts.crc32c
- Type: `Boolean`
- Default: `true`

Enable crc32c hashing via [sse4_crc32](https://gitnpm.com/sse4_crc32).*

* Note: Any issues installing this module on your system should be opened at their repository.

#### opts.md5
- Type: `Boolean`
- Default: `true`

Enable MD5 hashing.

### validateStream.test(algo, sum)

#### algo
- Type: `String`

The alogrithm to test the sum against ('crc32c' or 'md5').

#### sum
- Type: `String`

The sum to validate.
