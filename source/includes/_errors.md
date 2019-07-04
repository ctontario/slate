
# Errors

The CTO Registry API uses the following error codes:


Error Code | HTTP Status Code | Error Type | Description
---------- | -----------------|------------|-------------
<small>10100</small> | <small>400</small> | <small>INVALID_MESSAGE</small> | <small>The input is not valid</small>
<small>10101</small> | <small>400</small> | <small>INVALID_MIMETYPE</small> | <small>The file type is not accepted</small>
<small>10102</small> | <small>400</small> | <small>INVALID_RESPONSE</small> | <small>The response generated is not valid</small>
<small>20100</small> | <small>400</small> | <small>INVALID_USER_REGISTRATION_MESSAGE</small> | <small>The input for user registration is not valid</small>
<small>20101</small> | <small>400</small> | <small>USERNAME_DUPLICATE</small> | <small>User ID is already used</small>
<small>20102</small> | <small>400</small> | <small>INVALID_PASSWORD</small> | <small>Password is invalid (check password policy)</small>
<small>20103</small> | <small>400</small> | <small>EMAIL_DUPLICATE</small> | <small>Email is already used</small>
<small>20104</small> | <small>400</small> | <small>USER_NOT_FOUND</small> | <small>The user was not found</small>
<small>20105</small> | <small>400</small> | <small>USER_INSTITUTION_NOT_FOUND</small> | <small>The user institution was not found</small>
<small>20106</small> | <small>400</small> | <small>EMAIL_TOKEN_NOT_FOUND</small> | <small>The email validation token provided is not valid</small>
<small>20107</small> | <small>400</small> | <small>EMAIL_ALREADY_VALIDATED</small> | <small>The email has already been validated</small>
<small>20108</small> | <small>400</small> | <small>EMAIL_TOKEN_EXPIRED</small> | <small>The email validation token has expired.</small>
<small>20110</small> | <small>400</small> | <small>USER_INSTITUTION_ROLE_NOT_FOUND</small> | <small>The role requested was not found</small>
<small>20111</small> | <small>400</small> | <small>USER_INSTITUTION_ROLE_DUPLICATE</small> | <small>The role requested is already in the institution</small>
<small>20112</small> | <small>400</small> | <small>USER_INSTITUTION_ROLE_STATUS_INVALID</small> | <small>The role status requested is not valid</small>
<small>20120</small> | <small>400</small> | <small>INVALID_USER_ADD_INSTITUTION_MESSAGE</small> | <small>The input for adding a new institution is not valid</small>
<small>20121</small> | <small>400</small> | <small>INVALID_USER_UPDATE_INSTITUTION_MESSAGE</small> | <small>The input for updating a user institution is not valid</small>
<small>20122</small> | <small>400</small> | <small>USER_INSTITUTION_NOT_VERIFIED</small> | <small>The user institution requested has not been verified by the administration yet.</small>
<small>20130</small> | <small>400</small> | <small>USER_INSTITUTION_DUPLICATE</small> | <small>The institution requested is already in the account</small>
<small>20131</small> | <small>400</small> | <small>USER_INSTITUTION_NEEDS_CREATION</small> | <small>The user institution needs to be created before the requested action can be performed.</small>
<small>20140</small> | <small>400</small> | <small>USER_PASSWORD_UPDATE_FAILED</small> | <small>The password update failed</small>
<small>20141</small> | <small>400</small> | <small>USER_ACCOUNT_LOCKED</small> | <small>This account has been locked from too many failed login attempts.</small>
<small>20150</small> | <small>400</small> | <small>DOCUMENT_NOT_FOUND</small> | <small>The document requested could not be found</small>
<small>20151</small> | <small>400</small> | <small>DOCUMENT_DEFINITION_NOT_FOUND</small> | <small>The document definition from the requested document type could not be found</small>
<small>20152</small> | <small>400</small> | <small>DOCUMENT_DELETED</small> | <small>The document requested was marked as deleted</small>
<small>20500</small> | <small>400</small> | <small>LDAP_ENTRY_NOT_FOUND</small> | <small>The entry requested was not found</small>
<small>20501</small> | <small>400</small> | <small>LDAP_FAILED_TO_BIND</small> | <small>The attempt to bind the client failed</small>
<small>20502</small> | <small>400</small> | <small>LDAP_DUPLICATE_ENTRY</small> | <small>The user being created already existed in ldap</small>
<small>20503</small> | <small>400</small> | <small>LDAP_FAILED_TO_CREATE</small> | <small>The entry could not be created.</small>
<small>20504</small> | <small>400</small> | <small>LDAP_FAILED_TO_DELETE</small> | <small>The entry could not be deleted</small>
<small>20510</small> | <small>400</small> | <small>LDAP_FAILED_TO_MODIFY</small> | <small>The entry could not be updated.</small>
<small>21100</small> | <small>400</small> | <small>INVALID_INSTITUTION_REGISTRATION_MESSAGE</small> | <small>The input for institution registration is not valid</small>
<small>21101</small> | <small>400</small> | <small>INSTITUTION_NAME_DUPLICATE</small> | <small>Institution name is already used</small>
<small>21102</small> | <small>400</small> | <small>INSTITUTION_CODE_DUPLICATE</small> | <small>Institution code is already used</small>
<small>21103</small> | <small>400</small> | <small>INSTITUTION_NOT_FOUND</small> | <small>Institution not found</small>
<small>21104</small> | <small>400</small> | <small>INSTITUTION_ALTERNATE_NAME_DUPLICATE</small> | <small>Institution alternate name is already in use</small>
<small>21110</small> | <small>400</small> | <small>INSTITUTION_CODE_NOT_FOUND</small> | <small>The institution code does not exist</small>
<small>21120</small> | <small>400</small> | <small>INSTITUTION_TYPE_CODE_NOT_FOUND</small> | <small>Institution type code was not found</small>
<small>22100</small> | <small>400</small> | <small>COMMITTEE_NOT_FOUND</small> | <small>Committee not found</small>
<small>22101</small> | <small>400</small> | <small>COMMITTEE_CODE_NOT_FOUND</small> | <small>The committee code does not exist</small>
<small>22102</small> | <small>400</small> | <small>COMMITTEE_CODE_DUPLICATE</small> | <small>Committee code is already used</small>
<small>22103</small> | <small>400</small> | <small>COMMITTEE_NAME_DUPLICATE</small> | <small>Committee name is already used</small>
<small>22104</small> | <small>400</small> | <small>COMMITTEE_SHORTNAME_DUPLICATE</small> | <small>Committee short name is already used</small>
<small>22105</small> | <small>400</small> | <small>COMMITTEE_STREAMNAME_DUPLICATE</small> | <small>Committee stream name is already used</small>
<small>22110</small> | <small>400</small> | <small>COMMITTEE_USER_DUPLICATE</small> | <small>This user is already associated to the committee</small>
<small>22111</small> | <small>400</small> | <small>COMMITTEE_MEMBER_NOT_FOUND</small> | <small>The requested committee member was not found.</small>
<small>23104</small> | <small>400</small> | <small>STUDY_NOT_FOUND</small> | <small>Study not found</small>
<small>23105</small> | <small>400</small> | <small>QUICKSTART_SITE_NOT_FOUND</small> | <small>QuickSTART site not found</small>
<small>23106</small> | <small>400</small> | <small>QUICKSTART_SITE_NOT_READY</small> | <small>QuickSTART site not ready</small>
<small>23301</small> | <small>400</small> | <small>QUICKSTART_SITE_DUPLICATE</small> | <small>QuickSTART site with institutionId already exists on the specified QuickSTART application</small>
<small>23201</small> | <small>400</small> | <small>QUICKSTART_FIELD_DUPLICATE</small> | <small>QuickSTART field is already used</small>
<small>23302</small> | <small>400</small> | <small>QUICKSTART_REVIEW_NOT_COMPLETE</small> | <small>QuickSTART review must be completed before attempting the current action.</small>
<small>23303</small> | <small>400</small> | <small>QUICKSTART_REVIEW_NOT_APPLICABLE</small> | <small>The approval has either already been entered, or the approval is awaiting a sponsor response.</small>
<small>25020</small> | <small>400</small> | <small>ADMIN_VETTING_NOT_SET_FOR_MODERATION</small> | <small>The user institution is not set for moderation</small>
<small>25050</small> | <small>400</small> | <small>ADMIN_VETTING_CODE_NOT_RECOGNIZED</small> | <small>The vetting code used was not recognized</small>
<small>25051</small> | <small>400</small> | <small>ADMIN_VETTING_CODE_NOT_PERMITTED</small> | <small>The vetting code used is not permitted with the current status</small>
<small>26003</small> | <small>400</small> | <small>PRIVILEGE_NOT_FOUND</small> | <small>The privilege could not be found</small>
<small>26010</small> | <small>400</small> | <small>PRIVILEGE_TARGET_NOT_SET</small> | <small>The target for the privilege was not set</small>
<small>26011</small> | <small>400</small> | <small>PRIVILEGE_TARGET_NOT_FOUND</small> | <small>The target for the privilege could not be found in the system</small>
<small>26015</small> | <small>400</small> | <small>PRIVILEGE_DUPLICATE</small> | <small>The privilege was already assigned to the user</small>
<small>27001</small> | <small>400</small> | <small>TASKLOG_NOT_FOUND</small> | <small>The task log could not be found</small>
<small>27002</small> | <small>400</small> | <small>TASKLOG_ISSUE_NOT_FOUND</small> | <small>The task log issue could not be found</small>
<small>90100</small> | <small>401</small> | <small>UNAUTHENTICATED</small> | <small>Not authenticated to access this resource</small>
<small>90101</small> | <small>403</small> | <small>UNAUTHORIZED</small> | <small>Not authorized to access this resource</small>
<small>90102</small> | <small>401</small> | <small>AUTHENTICATION_EXPIRED</small> | <small>No longer authenticated to access this resource.  Please login again.</small>
<small>90103</small> | <small>403</small> | <small>PRIVILEGE_TARGET_REQUIRED</small> | <small>Resource was authorized, but specific privilege was not found for request data.</small>
<small>90110</small> | <small>400</small> | <small>AUTHENTICATION_FAILED</small> | <small>Wrong credentials: the authentication failed</small>
<small>90120</small> | <small>400</small> | <small>TOKEN_NOT_FOUND</small> | <small>The token used to access this resource was not found.</small>
<small>90121</small> | <small>400</small> | <small>INVALID_TOKEN</small> | <small>The token used to access this resource is not valid.</small>
<small>90130</small> | <small>400</small> | <small>ACCOUNT_UNVERIFIED</small> | <small>The account you are trying to access needs to be verified by an administrator.</small>
<small>90131</small> | <small>400</small> | <small>EMAIL_UNVALIDATED</small> | <small>The email used to create this account was not validated.</small>
<small>99000</small> | <small>400</small> | <small>CONNECTION_FAILED</small> | <small>The connection to the server could not be established</small>
<small>99001</small> | <small>400</small> | <small>ERROR</small> | <small>An error occurred while processing request</small>
<small>99011</small> | <small>400</small> | <small>ERROR_SEARCH_ENGINE_NOT_LIVE</small> | <small>The search engine is not live</small>
<small>99020</small> | <small>400</small> | <small>FILE_SIZE_EXCEEDS_LIMIT</small> | <small>The upload file size exceeds the permitted limit</small>
<small>99100</small> | <small>404</small> | <small>ROUTE_NOT_FOUND</small> | <small>The resource requested could not be located</small>
<small>99200</small> | <small>500</small> | <small>TASK_AUTH_NOT_FOUND</small> | <small>The task auth for this route was not found, but the route requires authorization.</small>
<small>99300</small> | <small>500</small> | <small>DATA_NOT_FOUND</small> | <small>The requested data was not found.</small>
<small>99999</small> | <small>501</small> | <small>NOT_IMPLEMENTED_YET</small> | <small>This feature is not implemented yet!</small>