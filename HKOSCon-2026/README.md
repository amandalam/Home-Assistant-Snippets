This folder contains items I shared in Hong Kong Open Source Conference 2026, including:

`Presentation_Deck.pdf`: the slides I presented

`Automation_MainDoorAnalysisSummary.yaml`: the automation example of taking a photo at the main door security camera and analyze it with Gemini, then push a notification to phone and update the MQTT topic summary field

`OpenClaw-Prompts/`

	AGENTS.md: 

		The prompts (written in Traditional Chinese - Cantonese) are to force all agents to use consistent way (exec command to call mcporter), especially useful for SLM (Small Language Model) which tool calling capability is limited

	CronJob_DailyStepsReport.md:

		The prompts (written in Traditional Chinese - Cantonese) are for creating a Daily Steps Report, by retrieving the history values of iPhone's step entity (change the entity name to yours). 

		Pre-requisite: You need to install the Home Assistant Companion App on your iPhone and grant its sensor values to Home Assistant

	CronJob_FlightsInCurrentAreaAnalysis.md:

		The prompts (written in Traditional Chinese - Cantonese) are for creating a Flights In Current Area report, by retrieiving the history values of the Flightradar's Current In Area entity (change the entity name to yours). 

		Pre-requisite: You need to install the Flightradar24 integration, define its Home coordinates, and the radius from the Home coordinates for flight tracking.

	CronJob_SecurityCameraAnalysis.md:

		The prompts (written in Traditional Chinese - Cantonese) are for creating a Security Camera analysis report, by retrieiving  the history values of the Main Door Summary Markdown field (change the markdown summary field name to yours).

		Pre-requisite: You need to install the MQTT integration and create the Main Door Summary Mardown topic. You also need set up AI integration so that you have the AI Task set up to take prompts for further analysis; and an automation to start the analysis when someone passes by --- see Automation_MainDoorAnalysisSummary.yaml for an example.

	CronJob_NewsAggregationExample.md:

		The prompts (written in Traditional Chinese - Cantonese) are for creating a daily news report on a specific topic and format it with sub-topic groupings, by submitting specific topic keywords as parameter to Google News RSS feed.  Here I use Disney as an example.

		Pre-requisite: You need to get web_search properly set up in OpenClaw so it will work.

All the files are licensed under GPL v3. See ../LICENSE file for details.