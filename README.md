# Data-Wilayah.js
Indonesian territory data in JavaScript

![indonesia map](https://kyotoreview.org/wp-content/uploads/Indonesia-map-678x381.jpg)

## Usage

```html
<!-- put this before your code -->
<script src="https://cdn.jsdelivr.net/gh/codenoid/Data-Wilayah.js/wilayah.js" type="text/javascript"></script>
<script>
for (const [key, value] of Object.entries(ID_PROVINSI)) {
  console.log(`Province Name : ${value}, Code : ${key}`);
}

function getAddress(nik) {
	// convert nik to string
    nik = nik.toString()
    
    var get_province = nik.substring(0,2)
    var get_kabupaten = nik.substring(2,4)
    var get_kecamatan = nik.substring(4,6)

    var address = []

    var kecamatan_name = ID_KECAMATAN[`${get_province}.${get_kabupaten}`][get_kecamatan];
    if ( kecamatan_name != undefined )
    	address.push(kecamatan_name)

    var kabupaten_name = ID_KABUPATEN[get_province][get_kabupaten];
    if ( kabupaten_name != undefined )
    	address.push(kabupaten_name)

    var provinsi_name = ID_PROVINSI[get_province];
    if ( provinsi_name != undefined )
    	address.push(provinsi_name)
    
    return address.join(", ")
}
console.log(getAddress("1101090310730001"))
</script>
```

## Source

https://github.com/cahyadsn/wilayah
