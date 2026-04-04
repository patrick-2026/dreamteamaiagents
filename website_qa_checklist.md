# 🌐 Global Website QA Checklist

Use this checklist to ensure every website preview is "Production Ready."

## 1. 📞 Contact & Critical Functionality
- [ ] **Phone Number Sync**: Verify that `href="tel:..."` matches the visible text label.
- [ ] **Email Links**: Verify `mailto:` links point to the correct business address.
- [ ] **Book Now / CTA Buttons**: Ensure all primary buttons lead to a functional booking tool or contact form.
- [ ] **Form Visibility**: Check that every form (Contact, Appointment, Newsletter) is fully visible on all viewports.
- [ ] **Required Fields**: Test that the "Submit" button is blocked and shows an error if required fields are empty.
- [ ] **Email Validation**: Confirm that the "Email" field correctly identifies and rejects invalid email formats.
- [ ] **Success Confirmation**: Test a form submission to verify that a "Success" or "Thank You" message appears after sending.
- [ ] **Spam Protection**: Verify if the form includes CAPTCHA or hidden anti-spam fields (Honeypots).

## 2. 🔗 Navigation & Links
- [ ] **Logo Link**: Clicking the logo should always return the user to the "Home" page.
- [ ] **Broken Links**: Scan for `404` errors or "Page Not Found."
- [ ] **Placeholder Links**: Check for `#` or `http://` placeholder URLs in the Main Nav and Footer.
- [ ] **Legal Links**: Verify Privacy Policy, Terms of Service, Accessibility, and Sitemap are active.
- [ ] **External Links**: Ensure social media or partner links open in a new tab (`target="_blank"`).

## 3. 🖼️ Visuals & Alignment
- [ ] **Section Spacing**: Ensure vertical padding between sections is balanced and consistent.
- [ ] **Horizontal Overflow**: Check that no elements cause a horizontal scrollbar on mobile devices.
- [ ] **Content Centering**: Verify headings and buttons are correctly centered on mobile/tablet views.
- [ ] **Image Rendering**: Ensure all images load from the CDN and none are broken "broken image" icons.

## 4. ✍️ Content & Copywriting
- [ ] **Spelling & Grammar**: Scan for typos, especially in large Hero headings.
- [ ] **Placeholder Text**: Ensure no "Lorem Ipsum" or "Coming Soon" remains.
- [ ] **Tone Consistency**: Verify that CTAs use consistent wording (e.g., all "Schedule Now" vs a mix of "Book Today").
- [ ] **Copyright Year**: Ensure the footer shows the current year (e.g., "© 2024" or "© 2025").

## 5. 📱 Mobile Responsiveness
- [ ] **Mobile Header**: Ensure the logo, phone icon, and hamburger menu have enough "breathing room" (padding).
- [ ] **Hero Banner**: Verify that text stays readable against the background image on small screens.
- [ ] **Button Target Size**: Buttons must be large enough to be easily tapped on mobile.
- [ ] **Menu Interaction**: Open and close the mobile menu to ensure it functions smoothly.

## 6. 🛠️ SEO & Technical
- [ ] **Heading Hierarchy**: Ensure exactly one `<h1>` per page.
- [ ] **Meta Tags**: Verify `<title>` and `<meta description>` are populated with site-relevant keywords.
- [ ] **Alt text**: Verify all informative images have `alt` tags for screen readers.
- [ ] **Console Errors**: Check the browser console (`F12`) for any `RefrenceError` or `TypeError` during load.

## 📁 7. Multi-Page & Template Consistency
- [ ] **Template Sampling**: For large sites, audit at least one page per "Type" (e.g., one location, one blog, one service).
- [ ] **Viewport Consistency**: Ensure the `<meta name="viewport">` tag is present and identical on every sub-page.
- [ ] **Mobile Alignment**: Verify that sub-pages don't have hardcoded fixed widths (e.g., 768px) that cause horizontal scrolling.
- [ ] **Universal Header/Footer**: Confirm the phone number and logo links remain functional and identical across the entire site.

---
*Created for automated QA assistance.*
