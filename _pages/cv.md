---
layout: default
permalink: /cv/
title: CV
nav: true
nav_order: 5
cv_pdf: /assets/pdf/CV_JinukMoon_Oct15_2026.pdf
---

<iframe id="cv-frame" title="CV" hidden></iframe>

<style>
  #cv-frame {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100vh;
    border: 0;
    z-index: 2000;
  }
</style>

<script>
  // A PDF opened directly runs no analytics, so desktop browsers show it in a
  // full-window frame over this page, looking like the PDF opened on its own,
  // and GA can time the reading (cv_read, value = visible seconds).
  // Phones and tablets still jump to the PDF: iOS renders only the first page
  // of an embedded PDF.
  window.addEventListener('DOMContentLoaded', function () {
    var pdf = '{{ page.cv_pdf | relative_url }}';
    var send = typeof gtag === 'function' ? gtag : function () {};

    if (navigator.pdfViewerEnabled !== true || matchMedia('(pointer: coarse)').matches) {
      var gone = false;
      var go = function () {
        if (gone) return;
        gone = true;
        location.replace(pdf);
      };
      send('event', 'cv_open', { method: 'redirect', event_callback: go });
      setTimeout(go, 1500);
      return;
    }

    var frame = document.getElementById('cv-frame');
    frame.addEventListener('load', function () {
      frame.focus(); // keys (Space, arrows, Ctrl+F) go to the PDF right away
    });
    frame.src = pdf;
    frame.hidden = false;
    document.title = pdf.split('/').pop();
    send('event', 'cv_open', { method: 'embed' });

    var since = Date.now();
    var flush = function () {
      if (since === null) return;
      var seconds = Math.min(Math.round((Date.now() - since) / 1000), 1800);
      since = null;
      if (seconds > 0) send('event', 'cv_read', { value: seconds });
    };
    document.addEventListener('visibilitychange', function () {
      if (document.hidden) flush();
      else since = Date.now();
    });
    window.addEventListener('pagehide', flush);
  });
</script>
