---
title: "Contact"
description: Contact. Do you have a question that you need an answer to or simply want to ask how we are doing. Fill out the form on our support page and we'll be sure to reply soon.
permalink: "/contact.html"
---

<form name="contact" netlify>
<p>Please send your message to {{site.name}}. We will reply as soon as possible!</p>
<div class="form-group row">
<div class="col-md-6">
<input class="form-control" type="text" name="name" placeholder="Name*" required>
</div>
<div class="col-md-6">
<input class="form-control" type="email" name="_replyto" placeholder="E-mail Address*" required>
</div>
</div>
<textarea rows="8" class="form-control mb-3" name="message" placeholder="Message*" required></textarea>    
<input class="btn btn-success" type="submit" value="Send">
</form>
