# Colour Contrast Checker

A tool to check and ensure colour contrast compliance with WCAG guidelines, built using SvelteKit.

## Overview

This Colour Contrast Checker helps designers and developers ensure their colour choices meet the Web Content Accessibility Guidelines (WCAG) contrast requirements. By providing an easy-to-use interface, it allows users to check and adjust colour combinations for better accessibility.

## Preview

<img width="409" alt="image" src="https://github.com/user-attachments/assets/9a91d97c-5b58-4d48-b0da-33a8751d4c70">

## Technology Stack

- SvelteKit

## Getting Started

1. Clone the repository
2. Install dependencies: `npm install`
3. Run the development server: `npm run dev`

## Why I Created This
During work on another project, I stumbled upon the Web Content Accessibility Guidelines (WCAG). I decided to create a tool that would make it easier for developers and designers to check and ensure their colour choices comply with these guidelines.

## Challenges Faced
One of the main challenges I encountered while developing this tool was understanding and implementing the mathematics behind colour contrast calculations. The WCAG guidelines use a specific formula to determine the contrast ratio between two colours, which involves converting RGB colours to relative luminance values and then calculating the ratio.
