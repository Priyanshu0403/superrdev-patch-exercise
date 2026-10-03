# NOTES

## Summary of Changes

I mainly focused on fixing the bugs that were affecting the actual user experience.

- Fixed the search query so the status filter works correctly and archived tasks don't show up incorrectly.
- Fixed the loading state so it doesn't stay stuck when an API request fails.
- Added a small debounce to search so the API isn't called on every single keystroke.
- Reset the page to 1 whenever the search or status filter is changed.
- Added basic validation for `page` and `pageSize` so invalid values don't cause the backend to crash.

## What I Chose Not to Change

I didn't change the overall structure or UI because I wanted to keep the changes focused on the reported bugs.

I also left pagination as it is. The backend currently gets the matching records and then handles pagination in memory. Moving this to database-level pagination would be better, but I felt it was outside the scope of this small patch.

## Biggest Remaining Risk

One thing I noticed but didn't change is the Thread.sleep() in TaskController. It is currently used to simulate a delay for short search queries.

It doesn't cause a functional issue right now, but it can become a problem if the application gets more traffic. Since the request thread stays occupied while sleeping, multiple users searching at the same time could consume the available server threads and make other API requests slower or even cause timeouts.

I left it unchanged because removing it wasn't necessary for the main bug fixes and I wanted to keep the changes focused. 

## Tools / AI Used

I used Claude to help me go through the code and understand a few of the issues, especially the debounce, and request handling.

I didn't blindly use the generated changes. I checked the code, made adjustments where needed, and tested the fixes locally before finalizing them.