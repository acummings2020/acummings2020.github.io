# /assets/

Drop static files here — anything you want to link to or embed on the site.

## Your CV
Put your CV in here as **`cv.pdf`** (lowercase). The link on the CV page
(`/cv`) points at `/assets/cv.pdf`, so once the file is committed and pushed
the download button will work automatically.

## Images for blog posts
Add images here (or in a subfolder like `assets/images/`) and reference them
in your posts:

```markdown
![Alt text describing the image]({{ site.baseurl }}/assets/images/my-chart.png)
```

This file (`assets/README.md`) is safe to keep — it isn't rendered on the site.
