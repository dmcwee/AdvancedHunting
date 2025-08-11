# Create Account Queries

The queries in this folder are an example of developing an Advanced Hunting query that can be used for a Custom Alert when accounts are created and granted high level permissions on a device.

## Scenario

Consider the scenario where a threat actor has gained initial access to and endpoint and wants to create an account they can use in the future to maintain persistence. Typically the attacker will want to ensure they have an account with administrative permissions so when they return in the future they already have the elevated permissions necessary.

For a SOC the goal would be to monitor for when a new account is created and added to the, or one of, administrator group(s). In order to do this the SOC must monitor for account creation & group membership updates.

Considering the account creation and adding the user to an admin group is typically done by a script or tool we can generally assume that the create and add events should happen in a very short time period.

## Queries

**[Query 1](CreateAccount-Query1.kql):** Grab all the Account events on devices so we can see what event types we care about.

**[Query 2](CreateAccount-Query2.kql):** Reduce the Account events to AccountCreated and AccountAddedToLocalGroup so we can look at these in more depth.

**[Query 3](CreateAccount-Query3.kql):** Reduce our initial results to just account created and get select fields. We will merge this into a single line with the Account added to group events shortly. Note: AccountSid in this event refers to the account created SID.

**[Query 4](CreateAccount-Query4.kql):** Assign the results of the query to a local scaler variable and add back the query for Account Added events as well as extending the query by parsing the JSON in the Additional Fields column to extract Group Name.

**[Query 5](CreateAccount-Query5.kql):** Next merge the scaler value & query using an inner join method. You can now see the Time the Account was created as well as the Time the Account was added to the local group.

**[Query 6](CreateAccount-Query6.kql):** Extend the query by calculating the time difference between when the account was created and when it was added to the local group. Also, reduce the output fields to just those we want to see: Created, Added, Account Name, Local Group, Device Id, Device Name, Created By.

**[Query Final](CreateAccount-QueryFinal.kql):** Finally filter out the default action of adding the user to the local Users group and include the Timestamp, ReportId, and InitiatingProcessAccountObjectId fields which are required for creating Custom NRT Detection.

## Account Scripts

There are four different scripts for creating an account locally available:

* [CreateAccount.cmd](./CreateAccount.cmd)
* [new-user.ps1](./new-user.ps1)
* [newUser.bat](./newUser.bat)
* [newUser.cmd](./newUser.cmd)