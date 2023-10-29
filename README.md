# AI_assistant
How it works:
1 - we are uploading audio file that contains some instructions about new task.
Ex:  "I want to take a nap on Friday. What time can I do that?"
2 - We are converting audio to text using whisperAi api(by OpenAI)
3 - We are paasing our text with request to chatgpt api using def get_questions_from_chatgpt(). Chatgpt is looking for available time
in your schedule(we are passing your schedule to chat gpt using google calnedar API) where it can insert your new task(in this case nap).
It's outputting your task, time for that task etc in following format:

 event = {
            "summary": "Nap Time",
            "location": "Somwhere Online",
            "description": "Some more details on this awesome event.",
            'colorId': 6,
            "start": {
                "dateTime": "2023-06-02T09:00:00+02:00",
                "timeZone": "Europe/Vienna",
            },
            "end": {
                "dateTime": "2023-10-18T17:00:00-04:00",
                "timeZone": "America/Detroit",
            },
            "recurrence": ["RRULE:FREQ=DAILY;COUNT=2"],
            "attendees": [
                {"email": "ilsankenzhebaev27@gmail.com"},
                {"email": "ik10@albion.edu"},
            ],
        }
        event = service.events().insert(calendarId="primary", body=event).execute()
        print(f"Event created {event.get('htmlLink')}")

4 - Now we will insert new task using using google calendar api. Pass output text that we got in step 3 to our calendar API, and it will 
insert it to your calendar right away, since output text from step 3 is already in "inser format for calendar API"
