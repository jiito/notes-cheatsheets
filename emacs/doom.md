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


### Weird rust-analyzer bug
* If you are working in a rust project, the langauge server will not work if the
   file is not tracked form the main, i.e. if it is not included with the `mod` keyword 



### Adding character at beg of multi-line 
1. Enter visiual line mode: `SHIFT V` or visiual block mode: `CTRL V`
2. Select the line you want to edit.
3. Insert text: `SHIFT i` 
4. `ESC`
