# Feedly CVE Insight Fetcher

A Python script that fetches articles from a Feedly stream and extracts CVE (Common Vulnerabilities and Exposures) insight cards for vulnerability intelligence gathering.

## Overview

This script automates the process of:
1. Fetching articles from a Feedly Enterprise stream over the last 24 hours
2. Extracting CVE IDs mentioned in those articles
3. Retrieving detailed CVE insight cards from the Feedly API
4. Saving each CVE insight card as an individual JSON file for analysis

## Features

- **Automatic pagination** using Feedly's continuation tokens to ensure all articles are retrieved
- **Batch processing** of CVE lookups (up to 100 CVEs per API call)
- **Rate limiting** to prevent API throttling
- **Error handling** for network issues and missing data
- **Clean console output** showing progress at each step
- **Individual JSON files** for each CVE insight card for easy analysis and integration

## Requirements

- Python 3.6 or higher
- `requests` library

## Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/feedly-cve-fetcher.git
cd feedly-cve-fetcher
```

2. Install required dependencies:
```bash
pip install requests
```

## Configuration

Before running the script, you need to configure the following variables in `feedly_cve_fetcher.py`:

```python
API_KEY = "APIKEYHERE"
STREAM_ID = "STREAMIDHERE"
```

### Getting Your API Key

1. Log in to your Feedly Enterprise account
2. Navigate to your account settings
3. Generate or copy your API token

### Finding Your Stream ID

Your stream ID can be found in the Feedly web interface URL when viewing a specific feed or category.

## Usage

Run the script from the command line:

```bash
python feedly_cve_fetcher.py
```

### Output

The script will:
1. Display progress information in the console
2. Create a `cve_insights/` directory (if it doesn't exist)
3. Save each CVE insight card as `CVE-XXXX-XXXXX.json`

Example output:
```
============================================================
Feedly CVE Insight Card Fetcher
============================================================
Stream ID: enterprise/securecyberdefensescdthr/category/...
Time range: Last 24 hours

Step 1: Fetching articles from stream...
Fetching page 1 of articles...
  Retrieved 100 articles (Total so far: 100)
Fetching page 2 of articles...
  Retrieved 45 articles (Total so far: 145)
No more pages to fetch.

Total articles fetched: 145

Step 2: Extracting CVE IDs from articles...
Found 23 unique CVE IDs

CVE IDs found:
  - CVE-2024-1234
  - CVE-2024-5678
  ...

Step 3: Fetching CVE insight cards...
Fetching CVE insights for batch 1 (23 CVEs)...
  Successfully fetched 23 CVE insight cards

Step 4: Saving CVE insight cards...

Saved 23 CVE insight cards to 'cve_insights/' directory

============================================================
Process completed successfully!
============================================================
```

## Customization

You can adjust the following parameters in the script:

- `NEWER_THAN`: Change the time window (default: -86400000 for 24 hours)
- `BATCH_SIZE`: Adjust CVE batch size (max: 100)
- `SLEEP_BETWEEN_REQUESTS`: Modify rate limiting delay (default: 0.5 seconds)


## Troubleshooting

**No articles found**: Verify your stream ID is correct and contains articles from the last 24 hours.

**No CVE IDs extracted**: Ensure articles in your stream contain CVE entity tags. Not all security articles may have CVE entities.

**API authentication errors**: Check that your API key is valid and has the correct permissions for Enterprise API access.

**Rate limiting**: If you encounter rate limiting, increase the `SLEEP_BETWEEN_REQUESTS` value.

## Contributing

This is a proof-of-concept script provided as-is. Feel free to fork and adapt it for your specific needs.

## License

© 2025 Feedly, Inc. All rights reserved.

**DISCLAIMERS.** THE API SCRIPTS ARE PROVIDED "AS IS" FOR YOUR INTERNAL BUSINESS USE ONLY. THE ENTIRE RISK AS TO THE QUALITY AND PERFORMANCE OF THE API SCRIPTS IS WITH YOU. YOU AGREE THAT YOUR USE OF THE API SCRIPTS WILL BE AT YOUR SOLE RISK. TO THE FULLEST EXTENT PERMITTED BY LAW, FEEDLY DISCLAIMS ALL WARRANTIES, EXPRESS OR IMPLIED, IN CONNECTION WITH THE API SCRIPTS AND YOUR USE THEREOF, INCLUDING, WITHOUT LIMITATION, THE IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE, AND NON-INFRINGEMENT. FEEDLY MAKES NO WARRANTIES OR REPRESENTATIONS ABOUT THE ACCURACY OR COMPLETENESS OF THE API SCRIPTS AND NO REPRESENTATIONS THAT THE API SCRIPTS ARE NOT OTHERWISE ENCUMBERED BY ANY THIRD PARTY LICENSE, INCLUDING ANY OPEN-SOURCE LICENSE. FEEDLY ASSUMES NO LIABILITY OR RESPONSIBILITY FOR ANY: (1) ERRORS, MISTAKES, OR INACCURACIES; (2) PERSONAL INJURY OR PROPERTY DAMAGE, OF ANY NATURE WHATSOEVER, RESULTING FROM YOUR USE OF THE API SCRIPTS; (3) ANY UNAUTHORIZED ACCESS TO OR USE OF API SCRIPTS; (4) ANY INTERRUPTION OR CESSATION OF TRANSMISSION TO OR FROM THE API SCRIPTS; (5) ANY BUGS, VIRUSES, TROJAN HORSES, OR THE LIKE WHICH MAY BE TRANSMITTED TO OR THROUGH THE API SCRIPTS BY ANY THIRD PARTY; OR (6) ANY ERRORS OR OMISSIONS IN THE API SCRIPTS OR FOR ANY LOSS OR DAMAGE OF ANY KIND INCURRED AS A RESULT OF THE USE OF THE API SCRIPTS.

**LIMITATION OF LIABILITY.** IN NO EVENT SHALL FEEDLY BE LIABLE FOR ANY DAMAGES. FURTHER, IN NO EVENT SHALL FEEDLY BE LIABLE FOR ANY CONSEQUENTIAL, INCIDENTAL OR INDIRECT DAMAGES, INCLUDING, WITHOUT LIMITATION, ANY LOSS OF DATA, OR LOSS OF PROFITS OR LOST SAVINGS, ARISING OUT OF USE OF OR INABILITY TO USE THE LICENSED PRODUCT, EVEN IF FEEDLY HAS BEEN ADVISED OF THE POSSIBILITY OF SUCH DAMAGES, OR FOR ANY CLAIM BY ANY THIRD PARTY.

YOU ACKNOWLEDGE THAT YOU HAVE READ AND UNDERSTAND THESE TERMS AND AGREE TO BE BOUND BY THEM. YOU FURTHER AGREE THAT THESE TERMS ARE THE COMPLETE AND EXCLUSIVE STATEMENT OF THE AGREEMENT BETWEEN YOU AND FEEDLY FOR THE USE OF THE API SCRIPTS, AND THESE TERMS SUPERSEDE ANY PRIOR AGREEMENT, ORAL OR WRITTEN, AND ANY OTHER COMMUNICATIONS RELATING TO THE SUBJECT MATTER HEREOF.

## Support

For issues related to the Feedly API, please contact Feedly support or refer to the [Feedly Developer Documentation](https://developers.feedly.com/).

## Author

Created by the Feedly Customer Success team to help security professionals automate vulnerability intelligence gathering.
