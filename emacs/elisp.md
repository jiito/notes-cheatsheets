# Elisp Language Notes

Here I will takes notes on how to use and configure doom emacs

**Evaluation Notation**
A Lisp expression that you can evaluate is called a _form_

### Eval

You can use `M-:` to evaluate an expression quickly

### Example: Getting the jira prefix

```lisp
(defun get-jira-prefix (iden)
  "Get the JIRA branch identifier from IDEN."
  (let ((prefix (string-match "[A-Za-z]+-[0-9]+" iden)))
    (if (not prefix)
        (message iden) (substring iden prefix  (match-end 0))
        )
    )
  )

(defun current-git-branch ()
  "Get the current git branch."
  (vc-git--symbolic-ref (buffer-file-name)))

(defun insert-branch-id()
  "Insert the ticket identifier at point"
  (interactive)
  (insert (format "[%s]: "  (get-jira-prefix (current-git-branch)) ))
  (evil-insert-state)
  (forward-char)
  )

(add-hook 'git-commit-setup-hook 'insert-branch-id)
```

### Hooks
