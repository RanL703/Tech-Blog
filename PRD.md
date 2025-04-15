# Project Requirements Document: Hugo Blog Customization

**Project Goal:** To customize the appearance and functionality of a Hugo blog using the Blowfish theme to better reflect the owner's personality and improve user experience.

## 1. Introduction

This document outlines the requirements for customizing a Hugo blog that utilizes the Blowfish theme. The primary focus is on visual enhancements, particularly color accents for dark and light modes, and modifications to the homepage to display recent blog posts.

## 2. Current State

The blog is currently built using Hugo and the Blowfish theme. The default theme configuration is in place. The homepage does not currently display any recent blog posts. A background image file, `bg.webp`, exists in the `assets/img/` folder.

## 3. Project Scope

This project includes the following customization tasks:

* **Color Accent Customization:**
    * Implement a purple and black color accent scheme for the dark mode of the blog.
    * Implement a warmer white, yellow, and orange color accent scheme for the light mode of the blog.
* **Homepage Update:**
    * Modify the homepage to display the 9 most recent blog posts.
    * Ensure each displayed post includes a relevant thumbnail image sourced from the post's content or front matter.
* **Background Implementation:**
    * Set the `bg.webp` file located in the `assets/img/` directory as the background for the entire website.

## 4. Detailed Requirements

### 4.1 Color Accent Customization

* **Dark Mode:**
    * Primary accent color should be a shade of purple (specific hex codes to be determined).
    * Secondary accent color should be black or a dark grey.
    * These accents should be applied to elements such as links, buttons, highlights, and other UI components as deemed appropriate for the Blowfish theme.
* **Light Mode:**
    * Primary accent colors should include shades of white, yellow, and orange.
    * The specific shades and their application to UI elements should create a warm and inviting feel.
    * Consider using these accents for links, buttons, highlights, and other relevant UI components within the Blowfish theme's design.

### 4.2 Homepage Update

* **Recent Posts Display:**
    * The homepage should display the 9 most recently published blog posts.
    * The order should be based on the `date` field in the front matter of each post, with the newest posts appearing first.
* **Thumbnails:**
    * Each displayed post should have a thumbnail image.
    * The system should prioritize using an image specified in the post's front matter (e.g., a field named `thumbnail` or `image`).
    * If no image is specified in the front matter, the system should attempt to extract the first relevant image from the post's content to use as the thumbnail.
    * The thumbnails should be appropriately sized and formatted for display on the homepage, maintaining visual consistency.
* **Layout:**
    * The layout of the recent posts on the homepage should be visually appealing and responsive across different screen sizes.

### 4.3 Background Implementation

* **Site-wide Background:**
    * The `bg.webp` file located in the `assets/img/` folder should be set as the background for the entire website.
    * The background should be implemented in a way that it scales appropriately across different screen sizes and resolutions.
    * Consideration should be given to how the background interacts with the foreground content to ensure readability.

## 5. Assets

* `assets/img/bg.webp`: This image file will be used as the website background.

## 6. Success Criteria

* The dark mode of the blog features a visually appealing purple and black accent scheme.
* The light mode of the blog features a warm white, yellow, and orange accent scheme.
* The homepage displays the 9 most recent blog posts with relevant thumbnails.
* The `bg.webp` image is successfully implemented as the website background across all pages.
* The customizations are responsive and function correctly on different devices and screen sizes.

## 7. Future Considerations (Out of Scope for this Project)

* Further customization of the Blowfish theme beyond color accents and homepage modifications.
* Implementation of new features or functionalities not currently present in the theme.
* Optimization for specific performance metrics.

This document serves as a starting point for the customization project. Further clarification or adjustments may be necessary as the project progresses.