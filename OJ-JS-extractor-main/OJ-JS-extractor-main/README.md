# Job Extractor – OnlineJobs.ph & JobStreet Philippines

A Google Chrome Manifest V3 extension that extracts one currently open job listing and exports it as JSON.

## Supported websites

- OnlineJobs.ph
- JobStreet Philippines (`ph.jobstreet.com`)
- JobStreet Philippines legacy/redirect domains (`jobstreet.com.ph`)

## Features

- Extracts an individual job detail page, not a list of search results.
- Uses structured `JobPosting` JSON-LD when the website provides it, then falls back to visible page text.
- Displays a formatted JSON preview.
- Copies JSON to the clipboard.
- Downloads a `.json` file.
- Runs locally in Chrome; no external API or server is used.

## Fields

Common fields:
- `platform`
- `job_id`
- `job_title`
- `employer`
- `location`
- `salary`
- `salary_disclosed`
- `employment_type`
- `hours_per_week`
- `experience_level`
- `date_posted`
- `posted_text`
- `skills`
- `description`
- `job_url`
- `extracted_at`
- `extraction_warnings`

JobStreet-specific fields:
- `job_category`
- `work_arrangement`
- `shift_schedule`
- `matched_skills`

`matched_skills` represents skills shown in JobStreet's "How you match" panel. Those are not necessarily the employer's mandatory requirements. The `skills` field is reserved for skills/qualifications identified as job requirements or supplied as structured job data.

Undisclosed salary is preserved as `"Undisclosed"` and `salary_disclosed` is `false`. Missing information is left as `null` or an empty array; the extension does not guess.

## Install on Windows 10/11

1. Download `job-extractor-onlinejobs-jobstreet.zip`.
2. Right-click the ZIP and choose **Extract All...**.
3. Open Google Chrome.
4. Enter `chrome://extensions` in the address bar.
5. Turn on **Developer mode** in the upper-right corner.
6. Click **Load unpacked**.
7. Select the extracted `onlinejobs-json-extractor` folder (the folder containing `manifest.json`).
8. Optionally pin the extension using Chrome's puzzle-piece menu.

## Use

1. Open an individual job detail page on OnlineJobs.ph or JobStreet Philippines.
2. Click the extension icon.
3. Click **Extract & Export Both**.
4. Review the JSON preview. Chrome will copy the JSON and open the file save dialog.

Use **Extract Only** if you want to inspect the result before copying or downloading.

## Troubleshooting

### The popup says the site is unsupported
Confirm the active tab is on `onlinejobs.ph`, `ph.jobstreet.com`, or a JobStreet Philippines domain.

### No job title was found
Open a single job detail page rather than a search-results page. Refresh the page and try again after the listing has fully loaded.

### Some fields are null
JobStreet can change its page structure, and some employers do not publish every detail. The extension uses a mix of structured data and visible page text. It leaves undetected fields empty instead of making up values.

### The extension does not update
Go to `chrome://extensions`, click the reload icon on the extension, and refresh the job page.

## Project files

- `manifest.json` — Chrome extension configuration and supported domains.
- `popup.html` — Popup layout.
- `popup.css` — Popup styling.
- `popup.js` — Extraction and export controls.
- `content.js` — Website detection and job-page extraction.
- `README.md` — Installation and usage instructions.

## Privacy

The extension only reads the current supported job page when you click an extraction button. It has no analytics, tracking, external API calls, or automatic background scraping.
