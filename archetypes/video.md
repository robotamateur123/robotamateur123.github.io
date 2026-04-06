+++
title = '{{ replace .File.ContentBaseName "-" " " | title }}'
date = '{{ .Date }}'
description = 'One-line summary for portfolio cards.'
draft = true
toc = true

[params]
youtube = 'YOUTUBE_VIDEO_ID'

[cover]
image = '/play-with-arduino/images/your-thumb.jpg'
alt = 'Project thumbnail'
+++

## Summary

Briefly describe the project and what viewers will learn.

## Watch the Video
{{< youtube-responsive id="VIDEO_ID" >}}

## Resources

### Hardware Purchase Links
- Item 1
- Item 2

### Wiring Diagram
![diagram-name](/section/images/diagram-name.png)

### Source Code
```cpp
// Add your Arduino code here
```
