---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - json

toc_footers:
  - <a href='https://github.com/icubam/icubam'>ICUBAM on GitHub</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - main
  - backoffice
  - messaging

search: true
---

# Introduction

Welcome to the ICUBAM API! ICU Bed Activity Monitor (ICUBAM) is an open-source project whose aim is to gather real-time data on intensive care unit (ICU) bed availability. This project was started in March 2020 to help managed the COVID-19 pandemic in French hospitals, but could be expanded to other healthcare systems using our API. You can use our API to access the ICUBAM database, which has data on ICU bed availability, as well as data on the ICUs we manage and the geographical regions where they reside. Our webpage rendering functions for the main server and admin server are also documented here under the respective "Rendering" sections.

ICUBAM has three different servers: the main application server, the admin portal (or "back office") server, and the messaging server. The APIs documented here are categorized by the server they are hosted on.

You can view code examples in the dark area to the right.

More information about ICUBAM and its source code can be found on <a href='https://github.com/icubam/icubam'>Github</a>.
