## IndexExchange

- UserSync entry point mentioned in Prebid JS: `https://js-sec.indexww.com/um/ixmatch.html`
- Eentry point domain: `js-sec.indexww.com`
- Type: `Iframe`
- Code Reference: https://github.com/prebid/Prebid.js/blob/master/modules/ixBidAdapter.js#L46
- Are GDPR params explicitly passed to end-point mentioned in PBJS? `NO`
- Are USP params explicitly passed to end-point mentioned in PBJS? `NO`
- Does script try to read GDPR params from publisher CMP? `YES`
- Does script try to read USP params from publisher CMP? `YES`
- User Cookie Name: `CMID`
- User Cookie Domain: `casalemedia.com`
- User Cookie expiry: `1 year`
- PubMatic `PugMaster` like end-point domain: `https://ssum-sec.casalemedia.com`

## Flow
- `ixmatch.html` has code to read consent from CMPs and to initiate the further user-syncup
- `ixmatch.html` initaes call to `https://ssum-sec.casalemedia.com/usermatch?` as an `iframe`. The Consent params are passed as query-params if those are available.
- `usermatch` endpoint seems to be hosted on `CloudFlare Worker`, it sets the User Cookie and in response returns the DSP pixels to be fired 
- Sample of first response below, User ID is shared with DSPs in query params
```
<html>
    <head>
        <title></title>
    </head>
    <body>
        <img src="https://ad4m.at/ad/sim/ix" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://dpm.demdex.net/ibs:dpid=23728&amp;dpuuid=Y2VzLLHsSQxXrfSjMFJ0AwAA%26700?gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://s.amazon-adsystem.com/dcm?pid=78af914c-e755-4b90-bded-1b172aedc763&amp;us_privacy=&amp;gdpr=&amp;gdpr_consent=&amp;id=Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://ups.analytics.yahoo.com/ups/55940/sync?_origin=1&amp;redir2=true&amp;uid=Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB&amp;gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://csync.loopme.me/?redirect=https%3A%2F%2Fdsum-sec.casalemedia.com%2Frum%3Fcm_dsp_id%3D24%26external_user_id%3D%7Bviewer_token%7D&amp;us_privacy=&amp;gdpr=&amp;gdpr_consent=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://pr-bh.ybp.yahoo.com/sync/casale/Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB?gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://cm.g.doubleclick.net/pixel?google_nid=index&amp;google_cm&amp;google_hm=Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB&amp;gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://cdn.indexww.com/ht/htw-pixel.gif?Y2VzLLHsSQxXrfSjMFJ0AwAA%26700" style="display:none" width="0" height="0" alt="" border="0"/>
    </body>
</html>
```
- Does DSP pixel redirects back to SSP endpoint like PubMatic's `PUG`? : `NO`
- Is there a call to SSP endpoint like PubMatic's `SPUG`? : `NO`
- Sample of `second` response below
```
<html>
    <head>
        <title></title>
    </head>
    <body>
        <img src="https://s.amazon-adsystem.com/dcm?pid=78af914c-e755-4b90-bded-1b172aedc763&amp;us_privacy=&amp;gdpr=&amp;gdpr_consent=&amp;id=Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://ups.analytics.yahoo.com/ups/55940/sync?_origin=1&amp;redir2=true&amp;uid=Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB&amp;gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://cm.g.doubleclick.net/pixel?google_nid=index&amp;google_cm&amp;google_hm=Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB&amp;gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://csync.loopme.me/?redirect=https%3A%2F%2Fdsum-sec.casalemedia.com%2Frum%3Fcm_dsp_id%3D24%26external_user_id%3D%7Bviewer_token%7D&amp;us_privacy=&amp;gdpr=&amp;gdpr_consent=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://pr-bh.ybp.yahoo.com/sync/casale/Y2VzLLHsSQxXrfSjMFJ0AwAAArwAAAIB?gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://ad4m.at/ad/sim/ix" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://dpm.demdex.net/ibs:dpid=23728&amp;dpuuid=Y2VzLLHsSQxXrfSjMFJ0AwAA%26700?gdpr_consent=&amp;us_privacy=&amp;gdpr=" style="display:none" width="0" height="0" alt="" border="0"/>
        <img src="https://cdn.indexww.com/ht/htw-pixel.gif?Y2VzLLHsSQxXrfSjMFJ0AwAA%26700" style="display:none" width="0" height="0" alt="" border="0"/>
    </body>
</html>
```
