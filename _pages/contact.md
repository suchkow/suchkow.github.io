---
title: 'Contacts'
description: "Email is the best way to get in touch."
permalink: /about/contacts
---


Email is the best way to get in touch: 

**{{ site.email }}**

<div class="tag-list copy-buttons">
<button class="btn btn-default" onclick="copyEmailtoClipboard('{{site.email}}')">Copy address</button>
<a href="mailto:{{site.email}}">Send email</a>
</div>

Alternative (RU Zone) email: [suchkow@internet.ru](mailto:suchkow@internet.ru)<br/>
LinkedIn: [linkedin.com/in/suchkow](https://www.linkedin.com/in/suchkow)<br/>
GitHub: [github.com/suchkow](https://github.com/suchkow)<br/>
Telegram: [t.me/suchkow](https://t.me/suchkow)<br/>
Phone and WhatsApp: [+7 917 930 1551](tel:+79179301551)<br/>


<script>
function copyEmailtoClipboard() {
    navigator.clipboard.writeText((arguments[0]));

}
</script>