The following is a list of the API names for Action Types, along with a list of parameters, and their validation requirements.


#### `extract_jsonpath`
- `jsonpath`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string

#### `extract_regex`
- `regex`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string

#### `extract_xpath`
- `xpath`: **required**, string
- `variable_name`: **required**, string
- `source`: string
- `default`: string

#### `send_request`
- `url`: **required**, string
- `content`: nullable, string
- `method`: nullable, in:POST,GET,OPTIONS,PUT,DELETE
- `headers`: nullable, string
- `skip_ssl_verification`: nullable, bool
- `variable_name`: string
- `timeout`: nullable, numeric, max:10000

#### `send_email`
- `sender`: string
- `recipient`: **required**, string
- `content`: string
- `is_html`: boolean
- `subject`: **required**, string

#### `modify_response`
- `content`: string
- `status`: string
- `headers`: string

#### `script`
- `script`: **required**, string

#### `rate_limit`
- `period`: **required**, int
- `count`: **required**, int

#### `condition`
- `input`: string
- `operator`: **required**, string, in:eq,neq,sw,ew,ct,nct,gt,gte,lt,lte
- `value`: string
- `action`: **required**, string, in:stop,continue

#### `google_sheets_add_row`
- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `values`: string, **required**
- `formula_mode`: bool

#### `google_sheets_update_row`
- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `values`: string, **required**
- `formula_mode`: bool

#### `google_sheets_get_values`
- `provider_id`: string, **required**
- `spreadsheet_id`: string, **required**
- `range`: string, **required**
- `variable_name`: **required**, string

#### `aws_s3_create_bucket`
- `provider_id`: string, **required**
- `region`: string, **required**
- `bucket_name`: string, **required**
- `canned_acl`: string, in:private,public-read,public-read-write,authenticated-read

#### `aws_s3_put_object`
- `provider_id`: string, **required**
- `region`: string, **required**
- `bucket_name`: string
- `object_key`: string, **required**
- `body`: string, **required**
- `canned_acl`: string, in:private,public-read,public-read-write,authenticated-read

#### `aws_s3_delete_object`
- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**

#### `aws_s3_get_object`
- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**
- `variable_name`: string, **required**, min:1

#### `aws_s3_get_object`
- `provider_id`: string, **required**
- `region`: string
- `bucket_name`: string, **required**
- `object_key`: string, **required**
- `variable_name`: string, **required**, min:1

#### `aws_cf_invalidate`
- `provider_id`: **required**, int
- `distribution_id`: **required**, string
- `paths`: **required**, string

#### `discord_send_message`
- `provider_id`: **required**, string
- `content`: **required**, string
- `username`: string
- `avatar_url`: url

#### `slack_send_message`
- `webhook_url`: **required**, url
- `raw`: bool
- `content`: **required**, string

#### `dropbox_create_folder`
- `provider_id`: string, **required**
- `path`: string, **required**

#### `dropbox_delete`
- `provider_id`: string, **required**
- `path`: string, **required**

#### `dropbox_download_file`
- `provider_id`: string, **required**
- `path`: string, **required**
- `variable_name`: string, **required**

#### `dropbox_upload_file`
- `provider_id`: string, **required**
- `path`: string, **required**
- `body`: string, **required**
- `mode`: string, **required**, in:add,overwrite,update

#### `dropbox_get_link`
- `provider_id`: string, **required**
- `path`: string, **required**
- `variable_name`: string, **required**

#### `image_resize`
- `source`: string, **required**
- `width`: string
- `height`: string
- `aspect_ratio`: bool, **required**
- `variable_name`: string, **required**

#### `ssh_run_command`
- `provider_id`: string, **required**
- `host`: **required**, string
- `port`: number, min:1, max:65535
- `username`: **required**, string
- `command`: **required**, string
- `variable_name`: string
