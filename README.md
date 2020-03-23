# Data-Wilayah.js
Indonesian territory data in JavaScript

![indonesia map](https://kyotoreview.org/wp-content/uploads/Indonesia-map-678x381.jpg)

## Usage

### NIK to Address

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
console.log(getAddress("1101090312740001"))
// Trumon, KAB. ACEH SELATAN, ACEH
</script>
```

### Use with select

```javascript
for (const [key, value] of Object.entries(ID_PROVINSI)) {
    $("#province_id").append(`<option value="${key}">${value}</option>`)
}
$("#province_id").on('change', function() {
    var province_id = $(this).val()
    $("#district_id").html('<option value="" selected>Unknown</option>')
    // bawa province_id untuk list kabupaten
    if (ID_KABUPATEN[province_id] != undefined) {
        for (const [key, value] of Object.entries(ID_KABUPATEN[province_id])) {
            $("#district_id").append(`<option value="${key}">${value}</option>`)
        }
        $("#subdistrict_id").html('<option value="" selected>Unknown</option>')
        $("#village_id").html('<option value="" selected>Unknown</option>')
    }
})
$("#district_id").on('change', function() {
    var province_id = $("#province_id").val()
    var district_id = province_id + "." + $(this).val()
    $("#subdistrict_id").html('<option value="" selected>Unknown</option>')
    // bawa district_id untuk list kecamatan
    if (ID_KECAMATAN[district_id] != undefined) {
        for (const [key, value] of Object.entries(ID_KECAMATAN[district_id])) {
            $("#subdistrict_id").append(`<option value="${key}">${value}</option>`)
        }
        $("#village_id").html('<option value="" selected>Unknown</option>')
    }
})
$("#subdistrict_id").on('change', function() {
    var province_id = $("#province_id").val()
    var district_id = $("#district_id").val()
    var subdistrict_id = `${province_id}.${district_id}.${$(this).val()}`
    console.log(subdistrict_id)
    $("#village_id").html('<option value="" selected>Unknown</option>')
    // bawa province_id + district_id + subdistrict_id untuk list desa/village
    if (ID_DESA[subdistrict_id] != undefined) {
        for (const [key, value] of Object.entries(ID_DESA[subdistrict_id])) {
            $("#village_id").append(`<option value="${key}">${value}</option>`)
        }
    }
})
```

## Source

https://github.com/cahyadsn/wilayah
