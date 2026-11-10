# Your Fashionables — সেটআপ নির্দেশিকা

এই প্রজেক্টটি Netlify-তে হোস্ট করার জন্য তৈরি। Frontend বাংলা এবং Hind Siliguri font ব্যবহার করে। পণ্য ও পোস্টের তথ্য Netlify Blobs-এ সংরক্ষিত হয়; ছবি Cloudinary-তে যায়। অর্ডার Facebook Messenger-এ নেওয়া হয়।

## ১) GitHub-এ ফাইল আপলোড
এই ZIP Extract করে সব ফাইল ও `netlify` এবং `admin` folder-সহ আপনার `mobile-image-gallery` repository-র root-এ upload করুন। GitHub-এ `Add file → Upload files` ব্যবহার করা যায়।

## ২) Netlify-তে deploy
Netlify-তে `Add new site → Import an existing project → GitHub` দিয়ে repository connect করুন। Build command ফাঁকা রাখুন; publish directory `.`। Deploy করুন।

## ৩) Netlify environment variables
Netlify Site configuration → Environment variables-এ নিচের চারটি variable যোগ করুন:

- `ADMIN_PASSWORD` — শক্তিশালী আলাদা admin password
- `SESSION_SECRET` — দীর্ঘ random secret (কমপক্ষে 32 অক্ষর)
- `CLOUDINARY_CLOUD_NAME` — আপনার Cloudinary cloud name
- `CLOUDINARY_API_KEY` — Cloudinary API Key
- `CLOUDINARY_API_SECRET` — Cloudinary API Secret

আপনার Cloudinary Cloud Name: `gyjmos8a`। API Secret কখনো frontend code, GitHub বা ChatGPT-তে প্রকাশ করবেন না। শুধু Netlify environment variables-এ দিন। এরপর Netlify-তে নতুন করে deploy করুন।

## ৪) Admin panel
`https://YOUR-SITE.netlify.app/admin/` খুলে `ADMIN_PASSWORD` দিয়ে login করুন। এখান থেকে একাধিক ছবি দিয়ে পোস্ট এবং ব্রা/প্যান্টি পণ্য যোগ করতে পারবেন। Public homepage-এ সেগুলো দেখা যাবে।

## ৫) গুরুত্বপূর্ণ
- Upload endpoint admin token যাচাই করে; Cloudinary secret server-side থাকে।
- শুধু JPG/PNG/WebP, প্রতিটি সর্বোচ্চ 5 MB; একটি পোস্টে সর্বোচ্চ 20টি ছবি।
- এই প্রাথমিক সংস্করণে পোস্ট/পণ্য publish ও delete করা যায়; edit, comment, like এবং image deletion-from-Cloudinary এখনো যোগ করা হয়নি।
- Netlify Blobs প্রথম deploy-এ initialize হবে। Deploy সম্পন্ন হওয়ার পর Admin panel ব্যবহার করুন।
- Cloudinary-তে আগের unsigned preset `GalleryUpload` এই implementation-এ ব্যবহার হয় না; server-side signed upload ব্যবহৃত হয়।
- Messenger destination link: https://www.facebook.com/share/1Dsg7o2T34/
- Facebook share URL কখনো কখনো সরাসরি Messenger conversation না খুলে Facebook share page খুলতে পারে। প্রয়োজনে আপনার Page-এর direct Messenger URL দিয়ে `app.js`, `admin` বা `index.html`-এর link বদলাবেন।
