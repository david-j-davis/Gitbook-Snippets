# HTML Emails

Static:

- Name image files as such: 'cw_project_image-name_300x200.jpg'
- Always use <table border="0" cellpadding="0" cellspacing=“0”…>
- use image style ‘display:block'
- Use &nbsp; for empty vertical <td> tags but not with horizontal empty <td> tags
- To center a table have a parent table with align center. You can also set the body to background color as well as use a parent parent table with width 100% and a background color. Refer to PGE bulletin project.
- float tables with ‘align=“left"'
- Refer to http://www.emailology.org/#3 for tags and attributes supported.
- place styles on td tags where appropriate
- Set paragraph padding and margin on all <p> tags as Outlook will collapse them.
- Set global styles at the <td> level when possible
- Don’t set any attributes on the <tr>
- IE renders image links with a border, include style ‘border:0px;'
- Image hack if it doesn’t listen to valign=“top” or “bottom”, set a style on the associated <td> to style="font-size:0px;line-height:0px;"

Responsive:

- use widths on td tags and not table tags
- use on table tags: style="border-collapse: collapse;mso-table-lspace: 0pt; mso-table-rspace:0pt; margin:0 auto;padding:0; -webkit-text-size-adjust:none;
- on image tags put width 100% and don’t set height;
- Some clients and some email marketing platforms will respect max-widths on td tags and image tags.
- use text align-center on table outer table tags to center td tags in android and ios
- valign td tags especially when aligning left or with images
- td align left for columns side by side don’t align left tables
