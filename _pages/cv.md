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
    left: 0;
    width: 100%;
    border: 0;
  }
</style>

<script>
  // A PDF opened directly runs no analytics, so desktop browsers show it inside
  // this page and GA can time the reading (cv_read, value = visible seconds).
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
    var top = document.getElementById('navbar').offsetHeight;
    frame.style.top = top + 'px';
    frame.style.height = 'calc(100vh - ' + top + 'px)';
    frame.src = pdf;
    frame.hidden = false;
    document.querySelector('footer').style.display = 'none';
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
