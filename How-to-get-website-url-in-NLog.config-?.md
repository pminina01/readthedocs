I create a NLog.config file ,I want to write log to database.
I edit this file.
<parameter name="@Url" layout="${aspnet-request:serverVariable=HTTP_URL}"></parameter>
<parameter name="@IpAddress" layout="${aspnet-request:serverVariable=REMOTE_ADDR}:${aspnet-request:serverVariable=REMOTE_PORT}"></parameter>
But in the database ,I didn't get url or address. 