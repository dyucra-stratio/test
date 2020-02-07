# Merchandiser service API
# **Introduction** 
 Merchandiser service API is a micro service responsable for create, edit, delete and customizer custom sort for the The Corte Ingles's site.  With this micro service, you should be able to specified the order of specific product from the catalog by a selected hierarchy. 

## **URLs** 

- All calls MUST have the prefix defined in the `BASE URL` 
- Parameters within the URL are `case_sensitive`. 

## **Request** 

* The API requires JSON input to be UTF-8 encoded, and generates UTF-8 encoded JSON output
## General Query Parameters 

* `limit`: This parameter restricts the number of objects returned. 
* `offset`: This parameter specifies the (0-based) index of the first object from a collection to be returned (i.e. all objects before this offset will be skipped). Together with 'limit', this value can be used to implement paging.

This example uses the limit and offset parameters to return four custom sorts of 'eci-product' site and '999.4168736013' hierarchy, starting with the third one:
- /merchandiser/v1/sites/eci-products/hierarchies/999.4168736013?offset=2&limit=4
### HTTP Request Headers
Note: header names marked with * are required.

HTTP Request Header            | Example Value        | Description
------------------------------ | -------------------- |-------------------------
User-Agent*                    | Mozilla/5.0 ...      | The client application implementing the network protocol for communication between the client and server. The header should identify theapplication, including the specific version of the application.
Content-Type                   | application/json     | Content-type, required for POST and PUT requests, only if a payload is sent in the HTTP body.
## **Response**
### Typical Status Codes
* `200 OK` - The request was successful
* `201 Created` - The request was successful and a resource was created
* `400 Bad Request` - The request could not be understood or was missing required parameters
* `404 Not Found` - Resource was not found
* `409 Conflict` - The request could not be completed due to a conflict with the current state of the resource (possibly caused by concurrent submits)

### Global Status Codes
The following status codes may be returned by any endpoint (therefore they are not listed on the individual endpoints):
* `405 Method Not Allowed` - Requested method is not supported for the specified resource
* `500 Internal Server Error` - An unexpected error occurred while processing the request

### Response Messages
- Error, warning, and information response messages (eg. validation errors, backend errors) are provided in JSON-Format. The HTTP Status code is set accordingly.



## Version: ${project.version}

### /merchandiser/v1/custom-sorts-fields/{siteId}

#### GET
##### Summary:

Export custom sort fields configuration

##### Description:

Export a customSort fields configuration

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| site | path | Site Id. | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | It returns a Custom Sort Field entity | [CustomSortFieldList](#customsortfieldlist) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### POST
##### Summary:

Import custom sorts fields configuration

##### Description:

Import a customSort fields configuration

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body | Custom Sort Field configuration to insert. | Yes | [CustomSortFieldList](#customsortfieldlist) |
| site | path | Site Id. | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [CustomSortFieldList](#customsortfieldlist) |
| 201 | Created | [CustomSortFieldList](#customsortfieldlist) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 409 | Conflict | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### /merchandiser/v1/export/custom-sorts

#### GET
##### Summary:

exportBySite

##### Description:

Exports the full Custom Sort configuration.

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| Site Id. | query | Site Id. | No | string |
| hierarchy | query | hierarchy | No | string |
| startDate | query | startDate | No | string |
| endDate | query | endDate | No | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | List of Custom Sort Objects | [CustomSortList](#customsortlist) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### /merchandiser/v1/import/custom-sorts

#### POST
##### Summary:

importBySite

##### Description:

Import a full custom sort configuration

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| completeCustomSortList | body | Custom Sort to insert. | Yes | [CustomSortList](#customsortlist) |
| removePrevious | query | removePrevious | No | boolean |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [CustomSortList](#customsortlist) |
| 201 | Created | [CustomSortList](#customsortlist) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### /merchandiser/v1/sites/{site}/custom-sorts

#### GET
##### Summary:

getAllCustomSort

##### Description:

It returns a list of Custom Sort

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| site | path | Site Id. | Yes | string |
| hierarchy | query | Hierarchy Id. | No | string |
| baseSort | query | Base Sort. | No | string |
| startDate | query | Filter by start date | No | string |
| endDate | query | Filter by end date | No | string |
| active | query | Show only active/inactive custom sorts | No | boolean |
| offset | query | Number of items to skip in the query | No | integer |
| size | query | Number of items to retrieve | No | integer |
| sortBy | query | sort filter: name:asc,endDate:desc | No | string |
| includeAllElements | query | includeAllElements | No | boolean |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | List of Custom Sort Objects | [CustomSortList](#customsortlist) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### POST
##### Summary:

New Custom Sort for a Site

##### Description:

It will create a new custom sort in an specific site.
The attribute 'active' in the CustomSort will be set as false in all cases due to bussines rule that not allow create an active CustomSort

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body | Custom Sort to insert. | Yes | [CustomSort](#customsort) |
| site | path | Site Id. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [CustomSort](#customsort) |
| 201 | Created | [CustomSort](#customsort) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 409 | Conflict | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### /merchandiser/v1/sites/{site}/custom-sorts-fields

#### GET
##### Summary:

Get custom sort fields configuration by site

##### Description:

Get a customSort fields configuration

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| site | path | Site Id. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | It returns a Custom Sort Field entity | [CustomSortField](#customsortfield) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### POST
##### Summary:

New custom sorts fields for a site

##### Description:

Create the custom sorts fields configuration for a site

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body | The new Custom Sort Field to insert. | Yes | [CustomSortField](#customsortfield) |
| site | path | Site id of the custom sort fields configuration. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [CustomSortField](#customsortfield) |
| 201 | Created | [CustomSortField](#customsortfield) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 409 | Conflict | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### PUT
##### Summary:

Update custom sort fields configuration by site

##### Description:

It updates a customSortFields configuration

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body | Custom Sort Fields to be updated. | Yes | [CustomSortField](#customsortfield) |
| site | path | Site Id. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Updated | [CustomSortField](#customsortfield) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 409 | Conflict | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### DELETE
##### Summary:

Delete custom sort fields configuration by site

##### Description:

It deletes a customSortFields configuration

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| site | path | Site Id. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 204 | No content |  |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### /merchandiser/v1/sites/{site}/custom-sorts/{customSortId}

#### GET
##### Summary:

getCustomSort

##### Description:

Return a CustomSort by Id

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| site | path | Site Id. | Yes | string |
| customSortId | path | customSortId. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | It returns a Custom Sort entity | [CustomSort](#customsort) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### PUT
##### Summary:

updateCustomSort

##### Description:

It updates a customSort

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body | Custom Sort to be updated. | Yes | [CustomSort](#customsort) |
| site | path | Site Id. | Yes | string |
| customSortId | path | customSortId to be updated. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | Updated | [CustomSort](#customsort) |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 409 | Conflict | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

#### DELETE
##### Summary:

deleteCustomSort

##### Description:

It deletes a CustomSort

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| site | path | Site Id. | Yes | string |
| customSortId | path | A customSortId to remove. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK |  |
| 204 | No content |  |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### /merchandiser/v1/sites/{site}/custom-sorts/{customSortId}/items

#### POST
##### Summary:

createCustomSortItem

##### Description:

It creates a customSort item

##### Parameters

| Name | Located in | Description | Required | Schema |
| ---- | ---------- | ----------- | -------- | ---- |
| body | body | Custom Sort to insert. | Yes | [ [CustomSortItem](#customsortitem) ] |
| customSortId | path | Custom sort id for adding custom sort items. | Yes | string |
| site | path | Site Id. | Yes | string |

##### Responses

| Code | Description | Schema |
| ---- | ----------- | ------ |
| 200 | OK | [ object ] |
| 201 | Created | [ [CustomSortItem](#customsortitem) ] |
| 400 | Bad Request | [MerchandiserErrors](#merchandisererrors) |
| 404 | Not found | [MerchandiserErrors](#merchandisererrors) |
| 500 | Internal Server Error | [MerchandiserErrors](#merchandisererrors) |

### Models


#### CustomSortField

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| creationDate | string |  | No |
| id | string |  | No |
| items | [ [CustomSortFieldItem](#customsortfielditem) ] |  | No |
| lastModification | string |  | No |
| site | string | CustomSort's site | No |

#### CustomSort

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| active | boolean | It's must not be provided in creation, because a CustomSort always be created as inactive. | Yes |
| baseSort | string | CustomSort's base sort | Yes |
| creationDate | string |  | No |
| customSort | boolean |  | No |
| endDate | string | CustomSort's end date, format: ISO 8601 | Yes |
| hierarchy | string | Hierarchy's id | Yes |
| id | string |  | No |
| items | [ [CustomSortItem](#customsortitem) ] | CustomSort's items | No |
| lastModification | string |  | No |
| name | string | CustomSort's name | Yes |
| site | string | CustomSort's site | No |
| startDate | string | CustomSort's start date, format: ISO 8601 | Yes |

#### CustomSortList

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| items | [ [CustomSort](#customsort) ] |  | No |
| total | integer | Total items for that site | No |

#### ImportStatus

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| errors | [ string ] |  | No |
| imported | [ string ] |  | No |
| totalImported | integer |  | No |
| totalWithError | integer |  | No |

#### CustomSortItem

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| id | string | Product ID | Yes |

#### MerchandiserErrors

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| debugMessage | string |  | No |
| errors | [ [Error](#error) ] |  | Yes |
| message | string |  | No |
| status | string |  | No |
| traceId | string |  | No |

#### Error

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| code | integer | Internal error code | No |
| field | string | Field where the error happens | No |
| message | string | Error message | No |
| possibleSolutions | string | Possible solution | No |

#### CustomSortFieldItem

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| displayName | string | The fields text in the table | No |
| path | string | Field path in the product configuration | No |
| searchOrder | integer | Position to show in the filter drop-down list | No |
| searchable | boolean | Can the user search by this field? | No |
| showOrder | integer | Position to show in the table | No |
| type | string | Type of the data in the document | No |
| typeData | string | Document's type additional data | No |
| visible | boolean | Show this field in the custom sort table? | No |

#### CustomSortFieldList

| Name | Type | Description | Required |
| ---- | ---- | ----------- | -------- |
| items | [ [CustomSortField](#customsortfield) ] |  | No |
| total | integer | Total items for that site | No |
