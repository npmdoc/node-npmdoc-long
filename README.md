# api documentation for  [long (v3.2.0)](https://github.com/dcodeIO/long.js#readme)  [![npm package](https://img.shields.io/npm/v/npmdoc-long.svg?style=flat-square)](https://www.npmjs.org/package/npmdoc-long) [![travis-ci.org build-status](https://api.travis-ci.org/npmdoc/node-npmdoc-long.svg)](https://travis-ci.org/npmdoc/node-npmdoc-long)
#### A Long class for representing a 64-bit two's-complement integer value.

[![NPM](https://nodei.co/npm/long.png?downloads=true)](https://www.npmjs.com/package/long)

[![apidoc](https://npmdoc.github.io/node-npmdoc-long/build/screenCapture.buildNpmdoc.browser._2Fhome_2Ftravis_2Fbuild_2Fnpmdoc_2Fnode-npmdoc-long_2Ftmp_2Fbuild_2Fapidoc.html.png)](https://npmdoc.github.io/node-npmdoc-long/build/apidoc.html)

![npmPackageListing](https://npmdoc.github.io/node-npmdoc-long/build/screenCapture.npmPackageListing.svg)

![npmPackageDependencyTree](https://npmdoc.github.io/node-npmdoc-long/build/screenCapture.npmPackageDependencyTree.svg)



# package.json

```json

{
    "author": {
        "name": "Daniel Wirtz",
        "email": "dcode@dcode.io"
    },
    "bugs": {
        "url": "https://github.com/dcodeIO/long.js/issues"
    },
    "dependencies": {},
    "description": "A Long class for representing a 64-bit two's-complement integer value.",
    "devDependencies": {
        "closurecompiler": "^1.6",
        "metascript": "~0",
        "testjs": "latest"
    },
    "directories": {},
    "dist": {
        "shasum": "d821b7138ca1cb581c172990ef14db200b5c474b",
        "tarball": "https://registry.npmjs.org/long/-/long-3.2.0.tgz"
    },
    "engines": {
        "node": ">=0.6"
    },
    "gitHead": "8cdc1f74ced4f771aa844f1cbc565b1d4c4451b8",
    "homepage": "https://github.com/dcodeIO/long.js#readme",
    "keywords": [
        "math"
    ],
    "license": "Apache-2.0",
    "main": "dist/long.js",
    "maintainers": [
        {
            "name": "dcode",
            "email": "dcode@dcode.io"
        }
    ],
    "name": "long",
    "optionalDependencies": {},
    "readme": "ERROR: No README data found!",
    "repository": {
        "type": "git",
        "url": "git+https://github.com/dcodeIO/long.js.git"
    },
    "scripts": {
        "build": "node scripts/build.js",
        "compile": "ccjs dist/long.js --compilation_level=SIMPLE_OPTIMIZATIONS --create_source_map=dist/long.min.map > dist/long.min.js",
        "compress": "gzip -c -9 dist/long.min.js > dist/long.min.js.gz",
        "make": "npm run-script build && npm run-script compile && npm run-script compress && npm test",
        "test": "node node_modules/testjs/bin/testjs tests/suite.js"
    },
    "version": "3.2.0"
}
```



# <a name="apidoc.tableOfContents"></a>[table of contents](#apidoc.tableOfContents)

#### [module long](#apidoc.module.long)
1.  [function <span class="apidocSignatureSpan">long.</span>fromBits (lowBits, highBits, unsigned)](#apidoc.element.long.fromBits)
1.  [function <span class="apidocSignatureSpan">long.</span>fromInt (value, unsigned)](#apidoc.element.long.fromInt)
1.  [function <span class="apidocSignatureSpan">long.</span>fromNumber (value, unsigned)](#apidoc.element.long.fromNumber)
1.  [function <span class="apidocSignatureSpan">long.</span>fromString (str, unsigned, radix)](#apidoc.element.long.fromString)
1.  [function <span class="apidocSignatureSpan">long.</span>fromValue (val)](#apidoc.element.long.fromValue)
1.  [function <span class="apidocSignatureSpan">long.</span>isLong (obj)](#apidoc.element.long.isLong)
1.  object <span class="apidocSignatureSpan">long.</span>MAX_UNSIGNED_VALUE
1.  object <span class="apidocSignatureSpan">long.</span>MAX_VALUE
1.  object <span class="apidocSignatureSpan">long.</span>MIN_VALUE
1.  object <span class="apidocSignatureSpan">long.</span>NEG_ONE
1.  object <span class="apidocSignatureSpan">long.</span>ONE
1.  object <span class="apidocSignatureSpan">long.</span>UONE
1.  object <span class="apidocSignatureSpan">long.</span>UZERO
1.  object <span class="apidocSignatureSpan">long.</span>ZERO



# <a name="apidoc.module.long"></a>[module long](#apidoc.module.long)

#### <a name="apidoc.element.long.fromBits"></a>[function <span class="apidocSignatureSpan">long.</span>fromBits (lowBits, highBits, unsigned)](#apidoc.element.long.fromBits)
- description and source-code
```javascript
function fromBits(lowBits, highBits, unsigned) {
    return new Long(lowBits, highBits, unsigned);
}
```
- example usage
```shell
...

Signed zero.

|                 |                 |
|-----------------|-----------------|
| **@type**       | *!Long*         |

#### Long.fromBits(lowBits, highBits, unsigned=)

Returns a Long representing the 64 bit integer that comes by concatenating the given low and high bits. Each is
assumed to use 32 bits.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| lowBits         | *number*        | The low 32 bits
...
```

#### <a name="apidoc.element.long.fromInt"></a>[function <span class="apidocSignatureSpan">long.</span>fromInt (value, unsigned)](#apidoc.element.long.fromInt)
- description and source-code
```javascript
function fromInt(value, unsigned) {
    var obj, cachedObj, cache;
    if (unsigned) {
        value >>>= 0;
        if (cache = (0 <= value && value < 256)) {
            cachedObj = UINT_CACHE[value];
            if (cachedObj)
                return cachedObj;
        }
        obj = fromBits(value, (value | 0) < 0 ? -1 : 0, true);
        if (cache)
            UINT_CACHE[value] = obj;
        return obj;
    } else {
        value |= 0;
        if (cache = (-128 <= value && value < 128)) {
            cachedObj = INT_CACHE[value];
            if (cachedObj)
                return cachedObj;
        }
        obj = fromBits(value, value < 0 ? -1 : 0, false);
        if (cache)
            INT_CACHE[value] = obj;
        return obj;
    }
}
```
- example usage
```shell
...
| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| lowBits         | *number*        | The low 32 bits
| highBits        | *number*        | The high 32 bits
| unsigned        | *boolean*       | Whether unsigned or not, defaults to 'false' for signed
| **@returns**    | *!Long*         | The corresponding Long value

#### Long.fromInt(value, unsigned=)

Returns a Long representing the given 32 bit integer value.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| value           | *number*        | The 32 bit integer in question
| unsigned        | *boolean*       | Whether unsigned or not, defaults to 'false' for signed
...
```

#### <a name="apidoc.element.long.fromNumber"></a>[function <span class="apidocSignatureSpan">long.</span>fromNumber (value, unsigned)](#apidoc.element.long.fromNumber)
- description and source-code
```javascript
function fromNumber(value, unsigned) {
    if (isNaN(value) || !isFinite(value))
        return unsigned ? UZERO : ZERO;
    if (unsigned) {
        if (value < 0)
            return UZERO;
        if (value >= TWO_PWR_64_DBL)
            return MAX_UNSIGNED_VALUE;
    } else {
        if (value <= -TWO_PWR_63_DBL)
            return MIN_VALUE;
        if (value + 1 >= TWO_PWR_63_DBL)
            return MAX_VALUE;
    }
    if (value < 0)
        return fromNumber(-value, unsigned).neg();
    return fromBits((value % TWO_PWR_32_DBL) | 0, (value / TWO_PWR_32_DBL) | 0, unsigned);
}
```
- example usage
```shell
...

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| value           | *number*        | The 32 bit integer in question
| unsigned        | *boolean*       | Whether unsigned or not, defaults to 'false' for signed
| **@returns**    | *!Long*         | The corresponding Long value

#### Long.fromNumber(value, unsigned=)

Returns a Long representing the given value, provided that it is a finite number. Otherwise, zero is returned.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| value           | *number*        | The number in question
| unsigned        | *boolean*       | Whether unsigned or not, defaults to 'false' for signed
...
```

#### <a name="apidoc.element.long.fromString"></a>[function <span class="apidocSignatureSpan">long.</span>fromString (str, unsigned, radix)](#apidoc.element.long.fromString)
- description and source-code
```javascript
function fromString(str, unsigned, radix) {
    if (str.length === 0)
        throw Error('empty string');
    if (str === "NaN" || str === "Infinity" || str === "+Infinity" || str === "-Infinity")
        return ZERO;
    if (typeof unsigned === 'number') {
        // For goog.math.long compatibility
        radix = unsigned,
        unsigned = false;
    } else {
        unsigned = !! unsigned;
    }
    radix = radix || 10;
    if (radix < 2 || 36 < radix)
        throw RangeError('radix');

    var p;
    if ((p = str.indexOf('-')) > 0)
        throw Error('interior hyphen');
    else if (p === 0) {
        return fromString(str.substring(1), unsigned, radix).neg();
    }

    // Do several (8) digits each time through the loop, so as to
    // minimize the calls to the very expensive emulated div.
    var radixToPower = fromNumber(pow_dbl(radix, 8));

    var result = ZERO;
    for (var i = 0; i < str.length; i += 8) {
        var size = Math.min(8, str.length - i),
            value = parseInt(str.substring(i, i + size), radix);
        if (size < 8) {
            var power = fromNumber(pow_dbl(radix, size));
            result = result.mul(power).add(fromNumber(value));
        } else {
            result = result.mul(radixToPower);
            result = result.add(fromNumber(value));
        }
    }
    result.unsigned = unsigned;
    return result;
}
```
- example usage
```shell
...

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| value           | *number*        | The number in question
| unsigned        | *boolean*       | Whether unsigned or not, defaults to 'false' for signed
| **@returns**    | *!Long*         | The corresponding Long value

#### Long.fromString(str, unsigned=, radix=)

Returns a Long representation of the given string, written using the specified radix.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| str             | *string*        | The textual representation of the Long
| unsigned        | *boolean &#124; number* | Whether unsigned or not, defaults to 'false' for signed
...
```

#### <a name="apidoc.element.long.fromValue"></a>[function <span class="apidocSignatureSpan">long.</span>fromValue (val)](#apidoc.element.long.fromValue)
- description and source-code
```javascript
function fromValue(val) {
    if (val /* is compatible */ instanceof Long)
        return val;
    if (typeof val === 'number')
        return fromNumber(val);
    if (typeof val === 'string')
        return fromString(val);
    // Throws for non-objects, converts non-instanceof Long:
    return fromBits(val.low, val.high, val.unsigned);
}
```
- example usage
```shell
...
Tests if the specified object is a Long.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| obj             | ***             | Object
| **@returns**    | *boolean*       |

#### Long.fromValue(val)

Converts the specified value to a Long.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| val             | *!Long &#124; number &#124; string &#124; !{low: number, high: number, unsigned: boolean}* | Value
| **@returns**    | *!Long*         |
...
```

#### <a name="apidoc.element.long.isLong"></a>[function <span class="apidocSignatureSpan">long.</span>isLong (obj)](#apidoc.element.long.isLong)
- description and source-code
```javascript
function isLong(obj) {
    return (obj && obj["__isLong__"]) === true;
}
```
- example usage
```shell
...
| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| str             | *string*        | The textual representation of the Long
| unsigned        | *boolean &#124; number* | Whether unsigned or not, defaults to 'false' for signed
| radix           | *number*        | The radix in which the text is written (2-36), defaults to 10
| **@returns**    | *!Long*         | The corresponding Long value

#### Long.isLong(obj)

Tests if the specified object is a Long.

| Parameter       | Type            | Description
|-----------------|-----------------|---------------
| obj             | ***             | Object
| **@returns**    | *boolean*       |
...
```



# misc
- this document was created with [utility2](https://github.com/kaizhu256/node-utility2)
