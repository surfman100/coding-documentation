# Javascript

## General tips on usage
- common service for ajax calls. handle errors, notifications etc

## Useful libraries

### Autonumeric
formats number as you type. need hidden field under unless you want to post as string :(. The HTML:
```
<input type="text" class="text-right autonumeric-format" />
<input type="number" class="text-right" name="Weights[][MaxStructural]:number" value="${weight[0].MaxStructural}" style="display:none"/>
```
And the Javascript:
```
autonumberFields = new AutoNumeric.multiple(".autonumeric-format", autoNumericOptions);
```
And on the update:
```
        //before serializing, set the raw value on the input number fields
        autonumberFields.forEach(function (element) {
            let raw = element.getNumber();
            let jqueryElement = $(element.domElement);
            jqueryElement.next('input').val(raw);
        });
```

### serializeJSON
Serialize form into JSON for a POST
```
let serializedJSON = form.serializeJSON();
let stringifiedJSON = JSON.stringify(serializedJSON, null, ' ')

function postJSON(url, data, callback) {
    $.ajax({
        url: url,
        data: data,
        cache: false,
        dataType: 'json',
        contentType: 'application/json; charset=UTF-8',
        processData: true,
        type: 'POST'
    }).done(function (returnValue) {
        if (typeof callback == "function") callback(returnValue); else console.error('invalid use of ajaxservice.postJSON');
    }).always(function (data, textStatus, jqXHR) {
        processNotifications(data, textStatus, jqXHR);
    });
}
```

## E6 Modules
Simply
```
function A(){
  //body
}

export { A ;
```
