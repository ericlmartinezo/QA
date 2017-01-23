# Web test Challenge

#### Test Request: Feature Aiport search feature
Engineers have improved the way airport options Origin and Destination populate the results when a user begins to type in the **From** and **To** edit fields. A regression test on the feature is need to make assure that the feature works as expected.

1. Verify default text "From" and "To" appears when the page loads.
2. When entering text context prediction generates choices.
3. List view should scrollable.
4. Selected airport replaces default text.
5. Pop window "See full airport list" launches after clicking the link.
6. Webpage version: v2.0nightly
7. Browser to test: Safari, Chrome, Firefox


#### Test Environment for: Safari

 OS version: 10.11.6 El Capitan.
 
 version: 9.1.3
 
 website: United Airlines
 
 url:  https://www.united.com/ual/en/us/

#### Manual test run
**Testsuite:** Choose airports

**case:** Choose origin airport option

**Preconditions:**
	Clear cookies if necessary
	User is on United Airlines home screen for the first time
	https://www.united.com/ual/en/us/	
  
| **Steps:**                                      		|  **Expected:** 															|
|-------------------------------------------------------|---------------------------------------------------------------------------|
|1. Click text field marked "From*".     				|	Text pops up "See full airport list" 									|
|2. Type in "New"					    				|	A list of available airports pops up 									|
|3. Scroll through the list using list scroll bar		|	List view scrolls airport choices remain visible 						|
|														|	Typed in text remains in the edit field 								|
|4. Mouse over the list of airports      				|	Mouse over the Airports highlights them in gray shadow 					|
|5. Click airport "New York, NY, US (jFK - Kennedy)"	|	Default text "From*" is replaced with "New York, NY, US (jFK - Kennedy)"|

#### UI Automation cucumber-capybara

**features/choose_airports.feature**

Scenario: As future traveler I enter departure and destination airport

	Given I am on the United Airlines Home screen
  
	When I choose departure airport
  
	Then I choose arrival airport



**step_definitions/choose_destination.rb**

Given(/^I am on the United Airlines Home screen$/) do
	view("X-UA-Compatible")
	end

	When (/^I choose departure airport$/) do
		find('clickable-text', :text => 'From*').click
		fill_in 'Origin', with: "pdx"
	end

	Then (/^I choose arrival airport$/) do
		find('clickable-text', :text => 'To*').click
		fill_in 'Destination', with: "Paris, FR"
	end
