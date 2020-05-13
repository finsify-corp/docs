# Services

You can access to the list of service provided by Finsify.

## HTTP Request

`GET https://assets.finsify.com/service.json`

## Structure description

| Key | Type | Description |
|---|---|---|
| id | integer | Service ID. |
| name | string | Name of service provided by Finsify Hub. |
| provider | string | Name of Finsify's partner. `finsify` is deploy by Finsify Hub. |
| media_path | string | URL to link of service's images. |
| cover_file_name | string | Cover file name. A cover always has 3 sizes: `small`, `medium` and `large`. |
| logo_file_name | string | Logo file's name |
| color	 | object | Colour code of service. |
| type | string | The type of services provided by Finsify Hub. Finsify currently supports `bank`, `statement` and `other`. |
| country_code | string | Service's country code. |
| has_balance | bool | 	Does service have available balance? |
| call_to_action | object | If there is no call_to_action, value is NULL |