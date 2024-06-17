---
title: "Bringing functional requirements to life: a puzzle lover's dream"
date: 2024-06-16
categories:
  - product
  - blog
tags:
  - technical
  - features
---

I dove into this project with minimal technical knowledge. But as part of my learning journey, I was committed to be the developer for my app, at least in its early stages. Learning to code in the timeframe I wanted to launch was not possible, so I took the next best option: using a no code app builder. 

Even without learning the syntax of any particular coding language, there was still a steep learning curve. To my surprise, most of this development work was exactly what I loved to do: solving puzzles! In building my app, I’ve practiced this cycle many times: understanding a functional requirement, breaking it down into smaller parts, implementing and testing it, and readjusting the logic until the requirement was met. 

Figuring out how to design and implement each feature was a fun challenge. Even a seemingly simple interaction from a user’s perspective might be broken down into dozens of requirements. And once you have the broken-down requirements, there might still be multiple workflows that bring the requirements to life. 

Due to this complexity, I’ll be honest and say I rarely get the technical implementation right the first time. I’m almost tired of hearing myself ask “why is it doing that?!” during testing. But this is also where the most exciting problem solving is found. The feeling of getting it to finally work the way you want is incredible. :smiley:

To illustrate a bit of the thinking that goes into each part of the app, here’s a non-exhaustive list of considerations for a simple “virtual game room” feature. Keep in mind this was only a small (and non-unique, as many other games have this as well) part of the entire app, so you can imagine how much longer this list truly is for the whole game!

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="60%" />
</colgroup>
<thead>
<tr class="header">
<th>User Actions</th>
<th>Functional Requirements</th>
<th>Implementation Units</th>
</tr>
</thead>
<tbody>
<tr>
<td markdown="span" rowspan="3" style="vertical-align:top">**Select a Game**</td>
<td markdown="span" style="vertical-align:top">Allow host to select a game</td>
<td markdown="span" style="vertical-align:top">
	- Create a “Select Game” button under the game title.<br>
	- Only allow the player to select the game if the player owns the game.<br>
	- If they don’t own any games, redirect them to the games shop.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Host must enter a name</td>
<td markdown="span" style="vertical-align:top">
	- Select game button opens a popup that prompts a name input.<br>
	- Only allow “Create Room” button to be clickable if the name input is at least 1 character long.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Go to game lobby</td>
<td markdown="span" style="vertical-align:top">
	- When the button on the name input popup (Create Room”) is clicked, the host is redirected to the game lobby.<br>
	- There must be at least one character in the name input before allowing “Create Room” to be clickable.<br>
	- When “Create Room” is clicked, the user’s info (player name) is saved.<br>
</td>
</tr>

<tr>
<td markdown="span" rowspan="4" style="vertical-align:top">**View game lobby**</td>
<td markdown="span" style="vertical-align:top">Room has a unique code that allows others to join it</td>
<td markdown="span" style="vertical-align:top">
	- When the host clicks “Create Room”, a 5 digit code is randomly generated.<br>
	- The code is presented in the game lobby screen.<br>
	- The code remains static while the room is active.<br>
	- The code is saved to the database alongside player name.<br>

</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Show who is in the room lobby</td>
<td markdown="span" style="vertical-align:top">
	- Game lobby dynamically updates when a new player joins the room with the new player’s name.<br>
	- New players are added in order.<br>
	- Show when the game is full and prompt to fill the room when it is not full.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Do not allow the game to start unless the required number of players is present</td>
<td markdown="span" style="vertical-align:top">
	- Add condition to the “Start Game” button to be clickable only when required players condition is met.<br>
	- Explain that more players need to be added in order to start the game.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Multiple games can take place simultaneously without interfering with each other</td>
<td markdown="span" style="vertical-align:top">
		- Any data references to players must use the unique game code.<br>
</td>
</tr>

<tr>
<td markdown="span" rowspan="4" style="vertical-align:top">**Join a room**</td>
<td markdown="span" style="vertical-align:top">Unique code allows a user to join a specific room</td>
<td markdown="span" style="vertical-align:top">
	- Create input for code and player name.<br>
	- Only allow “Join Game” button to be clickable if the inputted code is 5 characters long.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Cannot join a room that does not exist</td>
<td markdown="span" style="vertical-align:top">
	- Do not navigate to or create a game lobby if the code does not already exist.<br>
	- Provide the user with an alert that the room code is not valid.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Cannot join a room that is full</td>
<td markdown="span" style="vertical-align:top">
	- Do not navigate to a game lobby that is already has the required/max number of players.<br>
	- Provide user with an alert that the room is full.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Players must have a name</td>
<td markdown="span" style="vertical-align:top">
	- Only allow “Join Game” button to be clickable if the name input is at least 1 character long.<br>
	- The user’s info (player name) is saved when they click on “Join Game” and associated to the specific game they joined.<br>
</td>
</tr>

<tr>
<td markdown="span" rowspan="3" style="vertical-align:top">**Leave a room**</td>
<td markdown="span" style="vertical-align:top">When a player leaves the room, they no longer appear in the room screen</td>
<td markdown="span" style="vertical-align:top">
	- Indicate whether the player is in or out of the game room in the database.<br>
	- Ensure game lobby includes only those who are in the game room.<br>
	- Maintain the order of players.<br>
	- Do not display gaps in the list of players in the game lobby.<br>

</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">The leaving player’s assigned character is freed to be assigned to a new player</td>
<td markdown="span" style="vertical-align:top">
	- Ignore an exited player’s character when assigning a character to a new player.<br>
</td>
</tr>
<tr>
<td markdown="span" style="vertical-align:top">Cannot join a room that is full</td>
<td markdown="span" style="vertical-align:top">
	- Remove the player's status as host.<br>
	- Update the another player's status to host.<br>

</td>
</tr>

<tr>
<td markdown="span" style="vertical-align:top">**Rejoin a room**</td>
<td markdown="span" style="vertical-align:top">Allow players to rejoin the room if they drop part way through the game, and retain their progress</td>
<td markdown="span" style="vertical-align:top">
	- If rejoined to the game lobby, add them to the bottom of the existing player list, not their original position.<br>
	- Do not assign a character that has already been assigned to someone else during their absence from the room.<br>
	- Keep all existing data relating to their game progress (e.g. clues obtained) so it will remain when they rejoin.<br>
</td>
</tr>


</tbody>
</table>