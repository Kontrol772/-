# Growtopia Private Server Documentation

## Table of Contents

1. [Introduction](#introduction)
2. [Functions](#functions)
    * [ancientprice](#ancientprice)
    * [ancientdialog](#ancientdialog)
    * [loop_worlds](#loop_worlds)
    * [detected](#detected)

## Introduction

This documentation provides an in-depth overview of the Growtopia Private Server (GPS) code, focusing on the algorithms and implementations of complex functions. The server is built upon ENet, a reliable UDP network library, and utilizes the nlohmann::json library for data handling.

## Functions

### ancientprice

**Description:** This function returns the price in Diamond Locks for upgrading an ancient item based on its ID.

**Algorithm:**
* The function uses a `switch` statement to match the input ID with the corresponding price.
* If the ID matches an ancient item, the function returns the negative price.
* If the ID does not match an ancient item, the function returns 0.

**Code Example:**

```c++
int ancientprice(int z) {
	switch (z) {
	case 5078: case 5080: case 5084: case 5082: case 7166:
		return -50;
	case 5126: case 5144: case 5162: case 5180: case 7168:
		return -75;
	case 5128: case 5146: case 5164: case 5182: case 7170:
		return -100;
	case 5130: case 5148: case 5166: case 5184: case 7172:
		return -125;
	case 5132: case 5150: case 5168: case 5186: case 7174:
		return -200;
	case 5134: case 5152: case 5170: case 5188: case 9212:
		return -200;
	default:
		return 0;
	}
}
```

### ancientdialog

**Description:** This function generates a dialog string for the ancient altar based on the player's inventory and the ancient item they are upgrading.

**Algorithm:**
* The function calculates the price in Diamond Locks for upgrading the item using the `ancientprice` function.
* The function checks if the player has enough Diamond Locks in their inventory using the `inventory_contains` function.
* Based on the price and the player's inventory, the function constructs a dialog string with the appropriate text and buttons.

**Code Example:**

```c++
string ancientdialog(ENetPeer* peer, int ril) {
	int price = abs(ancientprice(ril)), ewe = inventory_contains(peer, 1796);
	return "\\nadd_textbox|`2- " + items[pInfo(peer)->ances].name + " (OK!)|" + (ewe >= price ? "\\nadd_textbox|`2- " + to_string(price) + " Diamond Locks (OK!)" : "\\nadd_textbox|`o- " + to_string(price) + " Diamond Locks (" + to_string(ewe) + "/" + to_string(price) + ")") + "|\\nadd_spacer|small|\\nadd_smalltext|`1The upgraded item will be untradeable|" + (ewe >= price ? "\\nadd_button|ancientaltar|`0Complete the ritual" : "") + "|\\nend_dialog|tolol12|Return||\\nadd_quick_exit";
}
```

### loop_worlds

**Description:** This function performs various world-related tasks and updates, including:

* **Beach Party Game:** Manages the beach party game timer and updates blocks and player states.
* **Server Restart:** Sends messages and handles server restart procedures.
* **Daily Login Rewards:** Displays the Daily Login dialog and handles daily reward resets.
* **Leaderboard Updates:** Updates the leaderboard and handles daily resets.
* **Events:** Manages event timers and updates event-related data.
* **Crypto Currency:** Updates crypto prices, inventory, and stats.
* **World Menu:** Updates the world menu and handles world loading.
* **Rainbow Nickname:** Updates the rainbow nickname effect.
* **Autofarm:** Handles autofarm tasks for players.
* **Pets:** Spawns and updates pet AI.
* **World Timers:** Handles world timer expiration.
* **Fishing:** Updates fishing status and handles fish catches.
* **Firehouse:** Manages the firehouse effect.
* **Valentine's Event:** Updates Valentine's event progress and effects.
* **Playmods:** Removes expired Playmods.
* **NPCs:** Updates NPC behavior and spawns.
* **Donation Box:** Handles donation box interactions.
* **World Gems Bonus:** Handles world gem bonus upgrades.
* **Cheats:** Applies and removes cheats for players.
* **World Locks Recycle Event:** Manages the World Locks Recycle Event.
* **Gacha System:** Handles Gacha interactions.
* **Redeem Code:** Handles redeem code management.
* **2FA:** Handles 2FA verification.
* **Mooncake Altar:** Handles Mooncake Altar interactions.
* **Guide Book:** Handles Guide Book interactions.
* **Wizard Quests:** Handles Legendary Wizard Quests.
* **Vending Hub:** Handles Vending Hub interactions.
* **Washing Machine:** Handles Washing Machine interactions.
* **Recycle Machine:** Handles Recycle Machine interactions.
* **Transmutabooth:** Handles Transmutabooth interactions.
* **Billboard:** Handles Billboard interactions.
* **Personalize Profile:** Handles player profile personalization.
* **Xenonite Crystal:** Handles Xenonite Crystal interactions.
* **Scarf of Seasons:** Handles Scarf of Seasons interactions.
* **Infinity Crown:** Handles Infinity Crown interactions.
* **Rift Wings:** Handles Rift Wings interactions.
* **Rift Cape:** Handles Rift Cape interactions.
* **Skin Color:** Handles player skin color customization.
* **Summerfest:** Handles Summerfest Event interactions.
* **Block De Mayo:** Handles Block De Mayo Event interactions.
* **Carnival Event:** Handles Carnival Event interactions.
* **Growganoth Event:** Handles Growganoth Event interactions.

**Algorithm:**
* The function uses a timer to check for specific events and conditions.
* Based on the timer and the current state of the game, the function calls other functions to handle the specific tasks.
* The function iterates through all connected players and worlds to perform the necessary updates.

**Code Example:**

```c++
void loop_worlds() {
	// ... code for handling various world-related tasks and updates ... 
}
```

### detected

**Description:** This function runs as a separate thread to continuously check for world-related events and perform updates.

**Algorithm:**
* The function runs in an infinite loop, calling the `loop_worlds` function every 600 milliseconds.

**Code Example:**

```c++
void detected() {
	while (true) {
		this_thread::sleep_for(chrono::milliseconds(600));
		loop_worlds();
	}
}
```

**Note:** This documentation only provides an overview of the code. Further details and specific function implementations are available in the actual source code. 
