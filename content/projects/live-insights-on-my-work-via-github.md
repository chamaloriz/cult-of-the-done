---
title: Creating my first MacOS app
created: 2025-10-20
tags:
  - success
  - macos
---
![[contributionbar-logo-light.png]]

I love checking my daily GitHub activity on my profile page. It's a nice way to see how I'm doing while giving me insights on my mental state over the course of a year. To make it easier to view, I came up with the idea of putting it in my macOS taskbar. In this article, I'll explain everything I discovered and learned while doing it. [here is the app link](https://github.com/chamaloriz/contribution-bar).

![[contributionbar-demo.png]]

It's my first time using cargo test to work on parts of my codebase

```rust

#[test]
pub fn generate_icon_file() {
	let testing_vec: Vec<u8> = vec![0, 1, 2, 3, 4, 5, 6];
	let img = generate_image(testing_vec);
	img.save("icon-test.png").expect("Failed to save image");
}

```


To round of the squares in the generated image I used a function to check the distance between two points. it works but it's not true corner rounding.

$$
\text{Distance} = \sqrt{(x_2 - x_1)^2 + (y_2 - y_1)^2}
$$

```rust
// here is the rust version

let distance_to_center = ((pixel_x as f64 - square_center.0 as f64).powi(2) + (pixel_y as f64 - square_center.1 as f64).powi(2)).sqrt();

```


I used an unofficial source for the data from [here](https://github.com/grubersjoe/github-contributions-api) its cached hourly but it's enough for the widget.

```json
// here is an example output from the api at
// GET : https://github-contributions-api.jogruber.de/v4/chamaloriz
{
   "total": {
      "2014": 1,
      "2015": 0,
      "2016": 0,
      "2017": 0,
      "2018": 3,
      "2019": 241,
      "2020": 567,
      "2021": 84,
      "2022": 895,
      "2023": 1018,
      "2024": 1016,
      "2025": 762
   },
   "contributions": [
      {
         "date": "2025-01-01",
         "count": 0,
         "level": 0
      },
      {
         "date": "2025-01-02",
         "count": 3,
         "level": 1
      }
      ...
   ]
}
```


To create the app for macos it's basically a folder name *app_name.app* when you add the .app extension it starts looking for the Info.plist file.

```xml
<!-- here is the most minimal version of that file for my purpose -->

<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
	<key>CFBundleExecutable</key>
	<string>contribution-bar</string>
	
	<key>CFBundleIconFile</key>
	<string>icon.icns</string>
	
	<key>CFBundleName</key>
	<string>ContributionBar</string>
	
	<!-- this makes the app disapear from the dock and tab -->
	<key>LSUIElement</key>
	<true/>
</dict>
</plist>
```


To run the app after downloading it and if the app is not signed you can use this command

```bash

# it removes quarantine flags from flag (to bypass security warnings). to remove the “damaged app” error.

xattr -cr /Applications/ContributionBar.app

```

If you try the app don't hesitate to start it [on github](https://github.com/chamaloriz/contribution-bar).