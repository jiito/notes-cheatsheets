# Doom Notes

### Rendering Markdown Preview 
[Reference](https://stackoverflow.com/questions/36183071/how-can-i-preview-markdown-in-emacs-in-real-time)
1. Install `impatient-mode`.
   `SPC : package-install RET impatient-mode`
2. Add configuration in config.el
```lisp 
  (defun markdown-html (buffer)
    (princ (with-current-buffer buffer
      (format "<!DOCTYPE html><html><title>Impatient Markdown</title><xmp theme=\"united\" style=\"display:none;\"> %s  </xmp><script src=\"http://strapdownjs.com/v/0.2/strapdown.js\"></script></html>" (buffer-substring-no-properties (point-min) (point-max))))
    (current-buffer)))
```
3. Tell impatient mode to use the filter: 
   ` SPC : imp-set-user-filter RET markdown-html RET`
4. Start HTTPD server 
    `SPC : httpd-start`
5. In the buffer you want to look at: 
   `SPC : impatient mode`
