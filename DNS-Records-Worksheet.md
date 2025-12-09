# DNS Records Worksheet - DropTheLeash GHL Setup
## Use this worksheet to track DNS records as you add them to cPanel

---

## WTW Community - DNS Records

### Funnel Domain: wtw.droptheleash.ca

| Record Type | Name/Host | Value/Target | TTL | Status |
|-------------|-----------|--------------|-----|--------|
| A | wtw | [GHL IP: _________] | 3600 | [ ] Added |
| CNAME | www.wtw | ghl.link | 3600 | [ ] Added |

### Community Domain: members-wtw.droptheleash.ca

| Record Type | Name/Host | Value/Target | TTL | Status |
|-------------|-----------|--------------|-----|--------|
| A | members-wtw | [GHL IP: _________] | 3600 | [ ] Added |
| CNAME | www.members-wtw | ghl.link | 3600 | [ ] Added |

### Email Domain: mg-wtw.droptheleash.ca

| Record Type | Name/Host | Value/Target | Priority | TTL | Status |
|-------------|-----------|--------------|----------|-----|--------|
| TXT (SPF) | mg-wtw | v=spf1 include:mailgun.org ~all | - | 3600 | [ ] Added |
| TXT (DKIM) | mx._domainkey.mg-wtw | [GHL DKIM Key: ___________________] | - | 3600 | [ ] Added |
| MX | mg-wtw | mxa.mailgun.org | 10 | 3600 | [ ] Added |
| MX | mg-wtw | mxb.mailgun.org | 10 | 3600 | [ ] Added |
| CNAME | email.mg-wtw | mailgun.org | - | 3600 | [ ] Added |

**WTW Verification Checklist:**
- [ ] Funnel domain verified in GHL (Sites > Settings > Domains)
- [ ] Community domain verified in GHL (Memberships > Communities > Settings)
- [ ] Email domain verified in GHL (Settings > Email Services)
- [ ] SSL certificate issued for wtw.droptheleash.ca
- [ ] SSL certificate issued for members-wtw.droptheleash.ca
- [ ] Test email sent successfully from mg-wtw.droptheleash.ca

---

## Aussie Community - DNS Records

### Funnel Domain: aussie.droptheleash.ca

| Record Type | Name/Host | Value/Target | TTL | Status |
|-------------|-----------|--------------|-----|--------|
| A | aussie | [GHL IP: _________] | 3600 | [ ] Added |
| CNAME | www.aussie | ghl.link | 3600 | [ ] Added |

### Community Domain: members-aussie.droptheleash.ca

| Record Type | Name/Host | Value/Target | TTL | Status |
|-------------|-----------|--------------|-----|--------|
| A | members-aussie | [GHL IP: _________] | 3600 | [ ] Added |
| CNAME | www.members-aussie | ghl.link | 3600 | [ ] Added |

### Email Domain: mg-aussie.droptheleash.ca

| Record Type | Name/Host | Value/Target | Priority | TTL | Status |
|-------------|-----------|--------------|----------|-----|--------|
| TXT (SPF) | mg-aussie | v=spf1 include:mailgun.org ~all | - | 3600 | [ ] Added |
| TXT (DKIM) | mx._domainkey.mg-aussie | [GHL DKIM Key: ___________________] | - | 3600 | [ ] Added |
| MX | mg-aussie | mxa.mailgun.org | 10 | 3600 | [ ] Added |
| MX | mg-aussie | mxb.mailgun.org | 10 | 3600 | [ ] Added |
| CNAME | email.mg-aussie | mailgun.org | - | 3600 | [ ] Added |

**Aussie Verification Checklist:**
- [ ] Funnel domain verified in GHL (Sites > Settings > Domains)
- [ ] Community domain verified in GHL (Memberships > Communities > Settings)
- [ ] Email domain verified in GHL (Settings > Email Services)
- [ ] SSL certificate issued for aussie.droptheleash.ca
- [ ] SSL certificate issued for members-aussie.droptheleash.ca
- [ ] Test email sent successfully from mg-aussie.droptheleash.ca

---

## cPanel Access Information

**cPanel URL:** ___________________________________
**Username:** ___________________________________
**Password:** (stored securely)

**Navigation Path:**
cPanel Dashboard > Domains Section > Zone Editor > Manage (next to droptheleash.ca)

---

## Notes & Troubleshooting Log

**Date:** ___________
**Issue:** ___________________________________
**Resolution:** ___________________________________

**Date:** ___________
**Issue:** ___________________________________
**Resolution:** ___________________________________

**Date:** ___________
**Issue:** ___________________________________
**Resolution:** ___________________________________

---

## Quick Reference: Common Issues

**DNS not propagating:**
- Wait 12-24 hours
- Check records entered correctly in cPanel
- Use DNS checker: whatsmydns.net

**SSL not issuing:**
- Verify domain first
- Wait 24 hours
- Toggle SSL off/on in GHL domain settings

**Email domain not verifying:**
- Ensure all 5 records added correctly
- Check for typos in DKIM key
- Verify MX priority is set to 10

**Domain shows "already connected":**
- Domain may be connected to different GHL account
- Contact GHL support to release domain
- Check for duplicate domain entries

---

## Setup Completion Timeline

| Task | Start Date | Completion Date | Notes |
|------|------------|-----------------|-------|
| WTW Funnel DNS | | | |
| WTW Community DNS | | | |
| WTW Email DNS | | | |
| Aussie Funnel DNS | | | |
| Aussie Community DNS | | | |
| Aussie Email DNS | | | |
| WTW Community Build | | | |
| Aussie Community Build | | | |
| Course Creation | | | |
| Test Purchases | | | |
| Go Live | | | |

**Total DNS Records:** 18 (9 per community)
