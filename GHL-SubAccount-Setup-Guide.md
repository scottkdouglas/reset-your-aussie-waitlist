# GoHighLevel Sub-Account Setup Guide
## DropTheLeash Communities: WTW & Aussie

This guide walks you through setting up two separate GoHighLevel sub-accounts with dedicated subdomains, email configuration, and community/course foundations.

**Subdomains to configure:**

**WTW Community:**
- Landing pages/funnels: `wtw.droptheleash.ca`
- Community portal: `members-wtw.droptheleash.ca`
- Email sending: `mg-wtw.droptheleash.ca`

**Aussie Community:**
- Landing pages/funnels: `aussie.droptheleash.ca`
- Community portal: `members-aussie.droptheleash.ca`
- Email sending: `mg-aussie.droptheleash.ca`

**Current setup:**
- Main domain: droptheleash.ca (active website)
- Email: laura@droptheleash.ca (GSuite/Google Workspace)

**Important Note:** GoHighLevel does not allow the same subdomain to be used for both Sites/Funnels AND Communities. You must use separate subdomains for each purpose.

---

## Part 1: Subdomain Setup for Websites/Funnels

**Purpose:** These subdomains will host your public landing pages, sales funnels, and course purchase pages for non-members.

### Step 1: Access Domain Settings in GHL Sub-Account

1. Log into your GoHighLevel sub-account
2. Navigate to: **Sites > Settings > Domains**
3. Click **"Connect a Domain"** or **"Add Domain"**

### Step 2: Choose Manual DNS Configuration

1. Select your desired product type (Funnels/Websites)
2. Enter your funnel subdomain: `wtw.droptheleash.ca` or `aussie.droptheleash.ca`
3. Click **"Add records manually"**
4. GHL will display the DNS records you need to add

### Step 3: DNS Records Required

You'll receive 2 DNS records from GoHighLevel:

**A Record:**
- Host: `wtw` (or `aussie`)
- Type: A
- Value: (GHL will provide IP, typically `34.120.54.74`)
- TTL: Automatic or 3600

**CNAME Record:**
- Host: `www.wtw` (or `www.aussie`)
- Type: CNAME
- Value: `ghl.link` (or similar target provided by GHL)
- TTL: Automatic or 3600

### Step 4: Add DNS Records to Your Domain Registrar

**For cPanel (NamesPro or other cPanel hosts):**

1. Log into your cPanel account
2. Locate the **Domains** section
3. Click on **Zone Editor**
4. Find `droptheleash.ca` and click **Manage**
5. Click **+ Add Record** (top right)
6. Select record type from dropdown (A, CNAME, etc.)
7. Add each record exactly as provided by GoHighLevel

**For other registrars (GoDaddy, Namecheap, Google Domains):**

1. Log into your domain registrar
2. Find the DNS Management or DNS Settings section
3. Add each record exactly as provided by GoHighLevel
4. Click Save after adding each record

**Important Cloudflare Note:**
If using Cloudflare, set Proxy status to **"DNS Only"** (gray cloud icon). GoHighLevel does not support Cloudflare Proxy.

### Step 5: Verify Domain in GHL

1. Return to GoHighLevel domain settings
2. Click **"Verify Domain"** or wait for automatic verification
3. DNS propagation can take up to 24 hours (usually 15-30 minutes)
4. SSL certificate will be automatically issued via Let's Encrypt

### Step 6: Set Up Community Subdomains

**Important:** You need separate subdomains for your community portals.

Repeat Steps 1-5 for the community subdomains:
- `members-wtw.droptheleash.ca`
- `members-aussie.droptheleash.ca`

These will use the same DNS record structure (A and CNAME records) but with different subdomain names.

### Step 7: Repeat for Second Sub-Account

Follow all steps for your second community (Aussie), setting up both:
- Funnel domain: `aussie.droptheleash.ca`
- Community domain: `members-aussie.droptheleash.ca`

---

## Part 2: Email Subdomain Setup with GSuite Integration

Since laura@droptheleash.ca uses Google Workspace on the root domain, you MUST use email subdomains for GoHighLevel sending.

### Recommended Email Subdomain Structure

**For WTW Community:**
- Email subdomain: `mg-wtw.droptheleash.ca`
- From address example: `hello@mg-wtw.droptheleash.ca`

**For Aussie Community:**
- Email subdomain: `mg-aussie.droptheleash.ca`
- From address example: `hello@mg-aussie.droptheleash.ca`

### Step 1: Access LC Email Domain Setup

1. In your GHL sub-account, go to: **Settings > Email Services**
2. Navigate to: **SMTP Service > Dedicated Domain and IP > Domain Configuration**
3. Click **"Add Domain"**

### Step 2: Enter Email Subdomain

1. Enter your email subdomain: `mg-wtw.droptheleash.ca`
2. Click continue to view DNS records

### Step 3: DNS Records for Email (5 Required)

GoHighLevel will provide 5 DNS records via Mailgun integration:

**TXT Record 1 (SPF):**
- Host: `mg-wtw` (subdomain only)
- Type: TXT
- Value: `v=spf1 include:mailgun.org ~all`

**TXT Record 2 (DKIM):**
- Host: `mx._domainkey.mg-wtw` (or similar pattern provided)
- Type: TXT
- Value: (GHL provides unique DKIM key)

**MX Record 1:**
- Host: `mg-wtw`
- Type: MX
- Priority: 10
- Value: `mxa.mailgun.org`

**MX Record 2:**
- Host: `mg-wtw`
- Type: MX
- Priority: 10
- Value: `mxb.mailgun.org`

**CNAME Record:**
- Host: `email.mg-wtw`
- Type: CNAME
- Value: `mailgun.org`

### Step 4: Add DNS Records to cPanel

**For cPanel (NamesPro):**

1. Log into your cPanel account
2. Go to **Domains > Zone Editor**
3. Click **Manage** next to `droptheleash.ca`
4. Click **+ Add Record** button
5. Add each of the 5 records:

**Adding TXT Records (SPF & DKIM):**
- Click **+ Add Record** > Select **TXT Record**
- Name: `mg-wtw` (for SPF) or `mx._domainkey.mg-wtw` (for DKIM)
- Record/Value: Paste the value from GHL
- TTL: 3600 or Automatic
- Click **Add Record**

**Adding MX Records:**
- Click **+ Add Record** > Select **MX Record**
- Name/Zone: `mg-wtw`
- Priority: 10
- Record/Destination: `mxa.mailgun.org` (then repeat for `mxb.mailgun.org`)
- TTL: 3600 or Automatic
- Click **Add Record**

**Adding CNAME Record:**
- Click **+ Add Record** > Select **CNAME Record**
- Name: `email.mg-wtw`
- Record/Target: `mailgun.org`
- TTL: 3600 or Automatic
- Click **Add Record**

6. Use only the subdomain portion in the Name/Host field (exclude `.droptheleash.ca`)
7. Click Save/Add Record after each entry

### Step 5: Verify Email Domain in GHL

1. Return to GoHighLevel domain configuration
2. Click **"Verify Domain"**
3. Send a test email to confirm functionality
4. Check spam score and deliverability

### Step 6: Repeat for Second Community

Set up `mg-aussie.droptheleash.ca` following Steps 1-5.

### Step 7: Configure Email Sending Preferences

1. Navigate to: **Settings > Email Services > Domain Selection**
2. Assign email domains to different email types:
   - **Workflow emails:** Choose your dedicated domain
   - **1:1 emails:** Choose your dedicated domain
   - **Campaign emails:** Set default domain
3. You can have up to 5 email domains per sub-account

---

## Part 3: Community Foundation Setup

### Step 1: Access Communities Section

1. In your GHL sub-account, go to: **Memberships > Communities**
2. Click **"Create New Community"**

### Step 2: Define Community Identity

**For WTW Community:**
1. Community Name: `Walk the Walk`
2. URL slug: `wtw` (or custom preference)
3. Short description: (Enter your community purpose)
4. Click **"Save"**

**For Aussie Community:**
1. Community Name: `Aussie Training Community` (or your choice)
2. URL slug: `aussie`
3. Short description: (Enter your community purpose)
4. Click **"Save"**

### Step 3: Customize Community Branding

1. Go to: **Memberships > Communities > Settings**
2. Upload branding assets:
   - **Favicon:** Your logo icon (16x16 or 32x32px)
   - **Cover Image:** Header banner image
   - **Logo:** Main community logo
3. Save changes

### Step 4: Configure Community Domain

**Critical:** Use your community-specific subdomain here, NOT your funnel subdomain.

1. In Community Settings, go to: **Domain Setup**
2. Enter your community subdomain: `members-wtw.droptheleash.ca` or `members-aussie.droptheleash.ca`
3. GHL may provide additional DNS records if needed
4. Add any new DNS records to cPanel Zone Editor (follow Part 1 instructions)
5. Click **"Update Domain"** in GHL
6. Wait up to 48 hours for DNS propagation
7. Verify domain connection

**Why Separate Domains?**
- Your funnel domain (`wtw.droptheleash.ca`) hosts public landing pages and sales pages
- Your community domain (`members-wtw.droptheleash.ca`) hosts the members-only portal
- This separation provides clear user experience and allows independent management

### Step 5: Create Groups Within Community

1. Navigate to: **Groups** section
2. Click **"Create Group"**
3. Enter:
   - Group name
   - Description
   - Privacy setting (Public or Private)
4. Assign moderators if needed
5. Save group

### Step 6: Add Communication Channels

1. In your community, click **"+ Add Channel"** in left panel
2. Create topic-based channels:
   - Welcome & Introductions
   - General Discussion
   - Course Q&A
   - Success Stories
3. Customize channel icons and privacy settings

### Step 7: Enable Gamification (Optional)

1. Go to: **Settings > Gamification & Rewards**
2. Set up member levels:
   - Bronze
   - Silver
   - Gold
3. Assign rewards and point thresholds
4. Enable **Leaderboard** if desired

---

## Part 4: Course Creation & Sales Setup

### Step 1: Create Your First Course

1. Go to: **Memberships > Courses**
2. Click **"+ Add Course"** or **"Create New Course"**
3. Enter:
   - Course title
   - Description
   - Content/lessons
4. Upload course materials (videos, PDFs, etc.)
5. Organize lessons into modules
6. Save course

### Step 2: Link Course to Community

1. Navigate to your community: **Memberships > Communities > [Your Community]**
2. Go to: **Learning** tab
3. Click **"+ Add Course"**
4. Select your created course from the library
5. Customize visibility settings:
   - **Public:** Visible to all (purchase required)
   - **Private:** Members only
6. Save

### Step 3: Set Up Paid Course Access

1. In the course settings, select **"Pricing"**
2. Choose payment model:
   - **One-time payment:** Lifetime access
   - **Recurring subscription:** Monthly/annual access
3. Enter price and select currency
4. Configure trial period (optional)
5. Enable **Test Mode** to validate payments before going live
6. Save pricing settings

### Step 4: Configure Payment Integration

1. Go to: **Settings > Payments**
2. Connect your payment processor:
   - **Stripe** (recommended)
   - NMI
   - Authorize.net
3. Click **"Connect Stripe"** and authorize
4. Configure payment methods to display:
   - Credit/Debit Cards
   - Apple Pay
   - Google Pay
   - Link
   - Amazon Pay
5. Payment methods are managed in GHL (not Stripe dashboard)

### Step 5: Set Up Paid Groups (Optional)

1. Navigate to: **Groups** in your community
2. Create or edit a group
3. Enable **"Paid Access"**
4. Choose payment model:
   - One-time: Unlimited access after payment
   - Recurring: Access continues while subscription active
5. Set price
6. Configure access settings:
   - **Public Group:** Auto-join after payment
   - **Private Group:** Admin approval required after payment

### Step 6: Create Course Landing Page for Non-Members

**Option A: Use Community Checkout Page**
1. Go to your course settings
2. Click **"Get Link"** button under course title
3. Copy the generated purchase link
4. Share this link on social media, email, etc.

**Option B: Build Custom Funnel**
1. Go to: **Sites > Funnels**
2. Click **"Create New Funnel"**
3. Choose a template or start from scratch
4. Add funnel steps:
   - **Landing page:** Course sales page
   - **Order form:** Checkout page (1-step or 2-step)
   - **Thank you page:** Post-purchase page
5. Edit landing page:
   - Add course details, benefits, testimonials
   - Include compelling CTA buttons
6. Configure order form:
   - Link to your course product
   - Select payment processor
   - Customize fields
7. Set funnel domain to your subdomain: `wtw.droptheleash.ca`
8. Publish funnel

### Step 7: Create Product in GHL

1. Go to: **Payments > Products**
2. Click **"Add New Product"**
3. Enter:
   - Product name (your course name)
   - Description
   - Price (one-time or recurring)
4. Link to course/community access
5. Save product

### Step 8: Set Up Automation for Course Access

1. Go to: **Automations > Workflows**
2. Create a new workflow:
   - **Trigger:** Payment received (Stripe)
   - **Action 1:** Add contact to course
   - **Action 2:** Send welcome email
   - **Action 3:** Add to community group (if applicable)
3. Test workflow in Test Mode
4. Activate workflow

### Step 9: Configure Member vs Non-Member Access

**For Members:**
1. Community members see courses in the Learning tab
2. Apply member discounts or free access in pricing settings
3. Set group-based access rules

**For Non-Members:**
1. Share direct purchase link or landing page URL
2. After payment, they gain course access
3. Optionally auto-enroll them in community after purchase (via workflow)

### Step 10: Test Complete Purchase Flow

1. Enable Test Mode in Stripe settings
2. Use Stripe test card: `4242 4242 4242 4242`
3. Complete test purchase as non-member
4. Verify:
   - Payment confirmation email sent
   - Course access granted
   - Community access granted (if applicable)
   - Workflows triggered correctly
5. Disable Test Mode when ready to go live

---

## Part 5: Complete Setup Summary

### Total DNS Records Per Community

**For WTW Community (6 subdomains total):**

**Funnel Domain:** `wtw.droptheleash.ca`
- A Record: `wtw` → GHL IP
- CNAME Record: `www.wtw` → ghl.link

**Community Domain:** `members-wtw.droptheleash.ca`
- A Record: `members-wtw` → GHL IP
- CNAME Record: `www.members-wtw` → ghl.link

**Email Domain:** `mg-wtw.droptheleash.ca`
- TXT Record (SPF): `mg-wtw` → v=spf1 include:mailgun.org ~all
- TXT Record (DKIM): `mx._domainkey.mg-wtw` → [GHL provided key]
- MX Record 1: `mg-wtw` → Priority 10 → mxa.mailgun.org
- MX Record 2: `mg-wtw` → Priority 10 → mxb.mailgun.org
- CNAME Record: `email.mg-wtw` → mailgun.org

**For Aussie Community:**
Repeat the same structure using `aussie`, `members-aussie`, and `mg-aussie` prefixes.

### User Journey Flow

**Non-Member Purchase Flow:**
1. Visitor lands on `wtw.droptheleash.ca` (sales funnel)
2. Completes course purchase via order form
3. Receives email from `hello@mg-wtw.droptheleash.ca`
4. Gets access credentials to `members-wtw.droptheleash.ca` (community portal)
5. Logs into community and accesses purchased course

**Member Experience:**
1. Member bookmarks `members-wtw.droptheleash.ca`
2. Logs in to see courses, groups, channels, events
3. Participates in community discussions
4. Accesses all learning materials in one portal

### Setup Order Recommendation

1. Set up email subdomains first (mg-wtw, mg-aussie)
2. Set up funnel subdomains (wtw, aussie)
3. Build initial landing page/funnel for course sales
4. Set up community subdomains (members-wtw, members-aussie)
5. Configure communities with groups and channels
6. Create and link courses
7. Test complete purchase and access flow
8. Go live with marketing campaigns

---

## Appendix A: cPanel Zone Editor Quick Guide (NamesPro)

### Accessing Zone Editor in cPanel

1. Log into your cPanel account at your hosting provider
2. Scroll to the **Domains** section (usually in the middle of the page)
3. Click on the **Zone Editor** icon
4. You'll see a list of domains - find `droptheleash.ca`
5. Click the **Manage** button next to the domain

### Adding Different Record Types

**General Process:**
- Click **+ Add Record** button (top right of the page)
- Select the record type from dropdown: A, CNAME, MX, TXT, etc.
- Fill in the required fields
- Click **Add Record** to save

**Field Names in cPanel:**
- **Name/Host/Zone**: The subdomain portion only (e.g., `wtw`, `mg-wtw`, `email.mg-wtw`)
- **Record/Value/Target**: The destination (IP address, domain name, or text value)
- **TTL**: Leave as default (3600) or Automatic
- **Priority**: Only for MX records (use 10)

### Important cPanel Notes

- Do NOT include the root domain (`.droptheleash.ca`) in the Name field
- cPanel automatically appends the root domain
- Example: For `wtw.droptheleash.ca`, enter only `wtw` in the Name field
- Changes can take 12-24 hours to propagate globally
- You can edit or delete records by clicking the respective buttons next to each record

### If You Don't See TXT Record Option

Some cPanel interfaces initially show only A, MX, and CNAME options:
1. Click **Manage** next to your domain
2. Click **+ Add Record**
3. Look for a dropdown or **Record Type** column
4. Select **TXT Record** from the full list of options

---

## Quick Reference: DNS Records Checklist

### For Each Funnel Subdomain (wtw, aussie):
- [ ] A Record (wtw or aussie → GHL IP)
- [ ] CNAME Record (www.wtw or www.aussie → ghl.link)

### For Each Community Subdomain (members-wtw, members-aussie):
- [ ] A Record (members-wtw or members-aussie → GHL IP)
- [ ] CNAME Record (www.members-wtw or www.members-aussie → ghl.link)

### For Each Email Subdomain (mg-wtw, mg-aussie):
- [ ] TXT Record (SPF)
- [ ] TXT Record (DKIM)
- [ ] MX Record 1 (mxa.mailgun.org)
- [ ] MX Record 2 (mxb.mailgun.org)
- [ ] CNAME Record (email.subdomain → mailgun.org)

### Total DNS Records Count
- **Per community:** 9 DNS records
- **Both communities:** 18 DNS records total
- All records added in cPanel Zone Editor under droptheleash.ca domain

---

## Troubleshooting Tips

**Domain not verifying:**
- Wait 24 hours for DNS propagation
- Check DNS records are entered exactly as provided
- Ensure no conflicting A, AAAA, or CNAME records exist
- Disable Cloudflare proxy if using Cloudflare

**SSL certificate not issuing:**
- Allow 24 hours for automatic SSL provisioning
- Re-verify DNS in GHL domain settings
- Toggle SSL off/on in domain settings

**Emails not sending:**
- Verify all 5 email DNS records are correct
- Send test email from GHL
- Check spam folder
- Use mail-tester.com to check spam score

**Course access not granted after payment:**
- Check workflow automation is active
- Verify product is linked to course
- Test payment integration in Test Mode first
- Check contact was created in GHL

**Member can't access community:**
- Verify domain is connected and verified
- Check member was added to correct group
- Ensure privacy settings allow access
- Check member's email verification status

---

## Additional Resources

- GoHighLevel Support Portal: help.gohighlevel.com
- HighLevel University: Free courses on community & course creation
- Course: "The Course Creator's Playbook" (available in HighLevel University)

---

## Notes

This guide covers foundational setup. Advanced features include:
- Affiliate program management
- Mobile app access for communities
- Advanced automation workflows
- Email sequences for course nurturing
- Webinar integration with communities
- Multiple pricing tiers and upsells

Your GoHighLevel account allows unlimited communities, making it easy to scale additional community projects in the future.
