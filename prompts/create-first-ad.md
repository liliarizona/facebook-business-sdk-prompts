# Prompt: Create Your First Facebook Ad Using Python Business SDK

**Description:**  
This prompt provides a code snippet and instructions for creating your first Facebook ad using the Facebook Python Business SDK.

---

## Python Code Example

```python
# Import the Facebook Business SDK modules
from facebook_business.api import FacebookAdsApi
from facebook_business.adobjects.adaccount import AdAccount
from facebook_business.adobjects.campaign import Campaign
from facebook_business.adobjects.adset import AdSet
from facebook_business.adobjects.adcreative import AdCreative
from facebook_business.adobjects.ad import Ad

# --- Placeholder values: replace with your actual credentials and IDs ---
APP_ID = '<YOUR_APP_ID>'
APP_SECRET = '<YOUR_APP_SECRET>'
ACCESS_TOKEN = '<YOUR_ACCESS_TOKEN>'
AD_ACCOUNT_ID = 'act_<YOUR_AD_ACCOUNT_ID>'  # Include the 'act_' prefix
PAGE_ID = '<YOUR_PAGE_ID>'

# Initialize the Facebook Ads API
FacebookAdsApi.init(APP_ID, APP_SECRET, ACCESS_TOKEN)

# 1. Create a new campaign
campaign = AdAccount(AD_ACCOUNT_ID).create_campaign(params={
    'name': 'My First Campaign',
    'objective': 'LINK_CLICKS',      # Objective can be changed as needed
    'status': 'PAUSED',              # Start as paused for safety
})
campaign_id = campaign['id']
print(f"Created Campaign ID: {campaign_id}")

# 2. Create a new ad set under the campaign
adset = AdAccount(AD_ACCOUNT_ID).create_ad_set(params={
    'name': 'My First Ad Set',
    'campaign_id': campaign_id,
    'daily_budget': 1000,            # Budget in minor units (e.g., cents)
    'billing_event': 'IMPRESSIONS',
    'optimization_goal': 'LINK_CLICKS',
    'bid_amount': 20,                # Bid in minor units (e.g., cents)
    'targeting': {
        'geo_locations': {'countries': ['US']},
        'age_min': 18,
        'age_max': 65,
    },
    'status': 'PAUSED',              # Start as paused for safety
    # Update these with desired times or remove for immediate start
    # 'start_time': '2025-10-23T00:00:00-0700',
    # 'end_time': '2025-11-01T00:00:00-0700',
})
adset_id = adset['id']
print(f"Created Ad Set ID: {adset_id}")

# 3. Create a new ad creative
creative = AdAccount(AD_ACCOUNT_ID).create_ad_creative(params={
    'name': 'My First Creative',
    'title': 'My First Ad',          # Deprecated in new API versions, use 'message' in object_story_spec
    'body': 'Try our product!',      # Deprecated, see above
    'object_url': 'https://www.example.com/',
    'link_url': 'https://www.example.com/',
    'page_id': PAGE_ID,
})
creative_id = creative['id']
print(f"Created Creative ID: {creative_id}")

# 4. Create the ad using the ad set and creative
ad = AdAccount(AD_ACCOUNT_ID).create_ad(params={
    'name': 'My First Ad',
    'adset_id': adset_id,
    'creative': {'creative_id': creative_id},
    'status': 'PAUSED',              # Start as paused for safety
})
ad_id = ad['id']
print(f"Created Ad ID: {ad_id}")
```

---

## Instructions

- Replace all `<YOUR_...>` values with your real credentials and IDs.
- Update the creative section to match your desired ad format and assets.
- Make sure you have the required permissions and your app is in Live mode.
- Run `pip install facebook-business` if you haven’t installed the SDK yet.

**Tip:** This is a minimal example for illustration and testing. Production code should implement proper error checking and logging.
