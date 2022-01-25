# postal-code-validation
Utility to validate postal codes

Find in `rules.json` conditions to validate Postal Code values  
according to the specific Country or to the specific State.

These rules are used to pre-validate WHOIS data before sending to the Registry.  
Some registries (e.g. the .ES) would validate the postal code also according to the declared STATE/Province,  
this is why the JSON includes rules which can be activated for a specific Country or for a specific State declared.

## how to read it

the JSON is served as an Array object, 
where each array node includes:
* a simple condition over the "country" property (2-letter ISO code) or over the "state" property (upper case name of the state)
  * rule is applied only if the condition matches with the input
* `$.pattern`: a regex to validate the postal code value against it
* `$.minLength`: the minimum length for the postal code (redundant, but useful to build specific controls over min length)
* `$.maxLength`: the maximum length for the postal code (redundant, but useful to build specific controls over max length)
* `$.example`: a value you can use as placeholder for the postal code field
* `$.dummyValue`: there are countries who only have one single valid postal code, in that case the `dummyValue` indicates that you can use that value as valid and go on



Example validation for Ireland (IE):

```
    {
        "when": {
            "propertyName": "country",
            "hasValues": [
                "ie"
            ]
        },
        "pattern": "^[A-Z0-9 ]{3,8}$",
        "minLength": 3,
        "maxLength": 8,
        "example": "D22 AF30"
    },
```
