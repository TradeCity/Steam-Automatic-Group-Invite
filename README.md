# Steam Automatic Group Invite - updated code.
The following code is in Beta stages and used for testing purposes only.
````
var steam_group_custom_url = "HexaDevelopment"; // ID
function InviteUserToSteamGroup(group_id)
{
	var params = {
		json: 1,
		type: 'groupInvite',
		group: group_id,
		sessionID: g_sessionID,
		invitee: g_rgProfileData.steamid
	};

	$.ajax({
		url: 'http://steamcommunity.com/actions/GroupInvite',
		data: params,
		type: 'POST',
		dataType: 'json'
	}).done(function(data) {
		if (data.duplicate) {
			console.log('[' + g_rgProfileData.steamid + '] The user are already in the group or have already received invites.');
		} else {
			console.log('[' + g_rgProfileData.steamid + '] Invite to Join Your Group.');
		}
	}).fail(function() {
		console.log('Error processing your request. Please try again.');
	});
}

function GetGroupData(steam_group_custom_url)
{
	return $.ajax({
		url: 'http://steamcommunity.com/groups/' + steam_group_custom_url + '/memberslistxml',
		data: { xml:1 },
		type: 'GET',
		dataType: 'xml'
	}).done(function(xml) {
		InviteUserToSteamGroup($(xml).find('groupID64').text());
	}).fail(function() {
		console.log('The request failed or the group custom URL is wrong.');
	});
}

GetGroupData(steam_group_custom_url);

````

# Updates Log
