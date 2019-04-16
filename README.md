# Okta-JMeter

This project provides a simple method to test the repsonse times which are being
achieved with Okta for both Authentication (AuthN) and Authorization (AuthZ).
The numbers shown are a rough indication as to the reponse times you would see
as a client from your current location and given the tenant configuration for your
test user.

Note these tools are not suitable for load testing an instance, this should be
done in conjunction with Okta Field Services.

## Requirements

To use the resources in this project you will require:
- An Okta tenant (You can get a free tenant at developer.okta.com)
- Apache JMeter (This project is based on JMeter 5)

## Tenant Configuration
Log into your tenant administrative account and complete the following actions:

### Create a test application
For this test we need an application for the user to be logging into. If you
already have an application deployed you can use this to give you a better view
of your end performance. If you do not have an application already deployed use
a public test application such as [oidcdebugger](https://oidcdebugger.com).

From the menu bar select 'Applications' then 'Add Application' and follow the
wizard. Be sure that you have correctly set the login redirect URIs and that the
grant types you wish to test have been checked.

From your application's general tab you will need to copy the client ID.

### Create a test user
This project stores the password for the user in the test file as such it is
recommended that you create a test user.

From the menu bar select 'Directory' or 'Users' then 'People'. Press 'Add
Person' and complete the form. Be sure to change the password field to 'set by
admin' and untick 'User must change password on first login'.

## JMeter configuration

Once you have downloaded and opened JMeter load the test file from this project
'AuthnAuthzResponseTiming.jmx'.

From the left hand panel select 'Okta Authn/Authz Test' this will show a number
of user defined variables in the right hand panel this is the configuration for
your test.

**Iteration-Count** This is the number of times you wish to execute the test,
default is 10.
**Okta-Tenant** This is you full Okta URL. yourcorp.oktapreview.com
**Client-Id** This is the client ID of your application you will be using for
the test.
**Redirect-Uri** This is the redirect Uri of the above application as configured
in Okta and where the AuthZ request will redirect traffic too.
**Test-User** This is the username of your test account.
**Test-User-Password** This is the password for the above user (note this is
stored in plain in your test file!).

Once you have completed the configuration, press the green run arrow in the menu
bar.

You can review the run by selecting 'Summary Report' from the left hand panel.
This will show you the response time for each step.

# Troubleshooting

If you encounter errors getting a successful test please use the Okta system log
to get the best explanation of what has occurred. If you want to examine the
requests and responses being sent by JMeter, from the left hand panel right click
'Detailed Result Tree' and select enable. When you next run the test each call
will be shown in that tree.

