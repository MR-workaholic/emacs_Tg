(custom-set-variables
 ;; custom-set-variables was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 '(show-paren-mode t)) 
(custom-set-faces
 ;; custom-set-faces was added by Custom.
 ;; If you edit it by hand, you could mess it up, so be careful.
 ;; Your init file should contain only one such instance.
 ;; If there is more than one, they won't work right.
 )

(add-hook 'org-moppde-hook (lambda () (setq truncate-lines nil)))
(put 'upcase-region 'disabled nil)

;;定义elpa源
(require 'package)
(add-to-list 'package-archives '("melpa" . "http://melpa.org/packages/") t)
(when (< emacs-major-version 24)
  (add-to-list 'package-archives '("gnu" . "http://elpa.gnu.org/packages/")))

(add-to-list 'package-archives
             '("elpy" . "https://jorgenschaefer.github.io/packages/"))

(package-initialize)


(add-to-list 'load-path "~/.emacs.d/elisp/")
(require 'color-theme)
(color-theme-initialize)
(color-theme-matrix)
(color-theme-classic)

;;不自动生成备份文件
(setq-default make-backup-files nil)

;;在标题栏显示buffer的名字
(setq frame-title-format "CZH@%b")

;; 关闭提示音
(setq visible-bell t)

;;;--- 显示行号
;; (require 'linum)
;; (setq linum-format "%3d ")
;;;--- 显示全局行号
(global-linum-mode t)
;;;--- 禁用启动信息
;; (setq inhibit-startup-message t)

;;;---对所有文件生效
(add-hook 'find-file-hooks (lambda () (linum-mode 1)))
;;;--- 显示列号
(setq column-number-mode t)
(setq line-number-mode t)

;;显示时间
;(display-time)

;;显示匹配的括号
(show-paren-mode t)

;;---- 在行首 C-k 时，同时删除该行
(setq-default kill-whole-line t)

;;解决linux中C-SPC切换输入法与emacs冲突
(global-unset-key (kbd "C-SPC"))
(global-set-key (kbd "M-SPC") 'set-mark-command)

;---------------------------------
;;- ido
;---------------------------------
;;这里是直接打开了ido的支持，在emacs23中这个是自带的.
(ido-mode t)
;;ido模式中不保存目录列表,解决退出Emacs时ido要询问编码的问题。
(setq ido-save-directory-list-file nil)


;---------------------------------
;;开机自动启动smex
;---------------------------------
(require 'smex)
 ; Not needed if you use package.el
(smex-initialize)
 ; Can be omitted. This might cause a (minimal) delay
 ; when Smex is auto-initialized on its first run.
(global-set-key (kbd "M-x") 'smex)
(global-set-key (kbd "M-X") 'smex-major-mode-commands)
;; This is your old M-x.
(global-set-key (kbd "C-c C-c M-x") 'execute-extended-command)

;---------------------------------
;;yansnippt 相关配置，需要放到ac配置前面,点击TAB键自动补全
;---------------------------------
(require 'yasnippet)
(setq yas/prompt-functions 
   '(yas/dropdown-prompt yas/x-prompt yas/completing-prompt yas/ido-prompt yas/no-prompt))
(yas/global-mode 1)
(yas/minor-mode-on) ; 以minor mode打开，这样才能配合主mode使用

;---------------------------------
;;ac：自动补全功能(最好结合其他框架使用)
;---------------------------------
(add-to-list 'load-path "~/.emacs.d/elisp/auto-complete")
(require 'auto-complete-config)
(add-to-list 'ac-dictionary-directories "~/.emacs.d/elisp/auto-cpmplete/ac-dict")
(ac-config-default)

;(set-face-background 'ac-candidate-face "lightgray")
;(set-face-underline 'ac-candidate-face "darkgray")
;(set-face-background 'ac-selection-face "steelblue") ;;; 设置比上面截图中更好看的背景颜色

;下面的是参考按网上的配置的
(setq ac-use-quick-help nil)
;(setq ac-auto-start 4) ;; 输入4个字符才开始补全
;(global-set-key "\M-/" 'auto-complete)  ;; 补全的快捷键，用于需要提前补全【貌似和撤销重复了】
;; Show menu 0.8 second later
(setq ac-auto-show-menu 0.8)
;; 选择菜单项的快捷键
(setq ac-use-menu-map t)
(define-key ac-menu-map "\C-n" 'ac-next)
(define-key ac-menu-map "\C-p" 'ac-previous)
;; menu设置为12 lines
(setq ac-menu-height 12)



;---------------------------------
;; ace jump mode major function  快速跳转到字母为x的单词前面
;---------------------------------
(add-to-list 'load-path "~/.emacs.d/elisp/ace-jump-mode")
(autoload
  'ace-jump-mode
  "ace-jump-mode"
  "Emacs quick move minor mode"
  t)
;; you can select the key you prefer to
(define-key global-map (kbd "C-c SPC") 'ace-jump-mode)

;--------------------------------
;
;---------------------------------

(add-to-list 'load-path "~/.emacs.d/elisp/emacs-async")
(autoload 
  'dired-async-mode 
  "dired-async.el" 
  nil 
  t)

(dired-async-mode 1)

;---------------------------------
;helm
;---------------------------------
(require 'helm)
(require 'helm-config)

(global-set-key (kbd "M-x") 'helm-M-x)

;; The default "C-x c" is quite close to "C-x C-c", which quits Emacs.
;; Changed to "C-c h". Note: We must set "C-c h" globally, because we
;; cannot change `helm-command-prefix-key' once `helm-config' is loaded.
(global-set-key (kbd "C-c h") 'helm-command-prefix)
(global-unset-key (kbd "C-x c"))

(define-key helm-map (kbd "<tab>") 'helm-execute-persistent-action) ; rebind tab to run persistent action
(define-key helm-map (kbd "C-i") 'helm-execute-persistent-action) ; make TAB works in terminal
(define-key helm-map (kbd "C-z")  'helm-select-action) ; list actions using C-z

(when (executable-find "curl")
  (setq helm-google-suggest-use-curl-p t))

(setq helm-split-window-in-side-p           t ; open helm buffer inside current window, not occupy whole other window
      helm-move-to-line-cycle-in-source     t ; move to end or beginning of source when reaching top or bottom of source.
      helm-ff-search-library-in-sexp        t ; search for library in `require' and `declare-function' sexp.
      helm-scroll-amount                    8 ; scroll 8 lines other window using M-<next>/M-<prior>
      helm-ff-file-name-history-use-recentf t)


(helm-mode 1)

;---------------------------------
;;projectile
;---------------------------------
(projectile-global-mode)
(setq projectile-completion-system 'helm)
(helm-projectile-on)

(setq projectile-switch-project-action 'helm-projectile)



;---------------------------------
;;gtags
;---------------------------------
;;修改PATH变量,可以参看笔记，在这里我是运用set去设置的
;(setenv "PATH" (concat "D:/emacs/.emacs.d/elisp/GNUglobal/bin;" (getenv "PATH")))

;;helm-gtags
(require 'helm-gtags)
(setq helm-gtags-ignore-case t
    helm-gtags-auto-update t
    helm-gtags-use-input-at-cursor t
    helm-gtags-pulse-at-cursor t
    helm-gtags-prefix-key "\C-cg"
    helm-gtags-suggested-key-mapping t)

;;; Enable helm-gtags-mode

(add-hook 'dired-mode-hook 'helm-gtags-mode)
(add-hook 'eshell-mode-hook 'helm-gtags-mode)

(add-hook 'c-mode-hook 'helm-gtags-mode)
(add-hook 'c++-mode-hook 'helm-gtags-mode)
(add-hook 'asm-mode-hook 'helm-gtags-mode)
(add-hook 'java-mode-hook 'helm-gtags-mode)


(defun set-helm-gtags-keybindings ()
  (define-key helm-gtags-mode-map (kbd "C-c g a") 'helm-gtags-tags-in-this-function) ;;查找在这个函数中的tags
  (define-key helm-gtags-mode-map (kbd "C-c g s") 'helm-gtags-select)      ;;查看已经被标示的tags
  (define-key helm-gtags-mode-map (kbd "M-."	) 'helm-gtags-dwim)       ;;跳转到定义
  (define-key helm-gtags-mode-map (kbd "M-,"    ) 'helm-gtags-pop-stack)  ;;返回上一个位置
  (define-key helm-gtags-mode-map (kbd "C-c g p") 'helm-gtags-previous-history) ;;上一步
  (define-key helm-gtags-mode-map (kbd "C-c g n") 'helm-gtags-next-history)   ;;下一步
  (define-key helm-gtags-mode-map (kbd "C-c g f") 'helm-gtags-find-pattern))   ;;查找使用该item的目标
(add-hook 'helm-gtags-mode-hook 'set-helm-gtags-keybindings)


;---------------------------------
;;function args 参考git的说明 https://github.com/abo-abo/function-args
;---------------------------------

(fa-config-default)
(add-to-list 'auto-mode-alist '("\\.h\\'" . c++-mode))
(add-to-list 'auto-mode-alist '("\\.hpp\\'" . c++-mode))
(add-to-list 'auto-mode-alist '("\\>\\'" . c++-mode)) ;;添加这一个后可以检测<>中的不带.h的头文件了
(set-default 'semantic-case-fold t)
;;(semantic-add-system-include "D:/Microsoft Visual Studio 10.0/VC/include" 'c++-mode)
(semantic-add-system-include "/usr/include/c++/5" 'c++-mode)
(semantic-add-system-include "/usr/include/x86_64-linux-gnu/c++/5" 'c++-mode)
(semantic-add-system-include "/usr/include/c++/5/backward" 'c++-mode)
(semantic-add-system-include "/usr/lib/gcc/x86_64-linux-gnu/5/include" 'c++-mode)
(semantic-add-system-include "/usr/local/include" 'c++-mode)
(semantic-add-system-include "/usr/lib/gcc/x86_64-linux-gnu/5/include-fixed" 'c++-mode)
(semantic-add-system-include "/usr/include/x86_64-linux-gnu" 'c++-mode)
(semantic-add-system-include "/usr/include" 'c++-mode)
;(semantic-add-system-include "/home/czh/Advanced_Programming_in_the_Unix_Environment/apue.3e/include" 'c++-mode)


;---------------------------------
;;company-mode 又一个自动完成，两种模式：Clang与gtags
;---------------------------------

(add-to-list 'load-path "~/.emacs.d/elisp/company-mode/")
(require 'company)
(add-hook 'after-init-hook 'global-company-mode)

;;To use company-mode with Clang, add this configuration
;(setq company-backends (delete 'company-semantic company-backends))
;(define-key c-mode-map  [(tab)] 'company-complete)
;(define-key c++-mode-map  [(tab)] 'company-complete)

;-------------------------
;; company-c-headers C语言头文件的自动补全
;--------------------------
(add-to-list 'company-backends 'company-c-headers)
;(add-to-list 'company-c-headers-path-system "/usr/include") ;总是报错，不知道为什么,但是可以使用

;; C++ auto completion mode
(require 'auto-complete)
(require 'auto-complete-config)
(ac-config-default)
;a function which initializes auto-complete-c-headers and get called for c/c++ hooks  在shell中运用gcc -xc++ -E -v -  去查看头文件位置 现在只能提示C的头文件
(defun my:acc-c-header-init ()
  (require 'auto-complete-c-headers)
  (add-to-list 'ac-sources 'ac-source-c-headers)
  (add-to-list 'achead:include-directories '"/usr/include/c++/5
 /usr/include/x86_64-linux-gnu/c++/5
 /usr/include/c++/5/backward
 /usr/lib/gcc/x86_64-linux-gnu/5/include
 /usr/local/include
 /usr/lib/gcc/x86_64-linux-gnu/5/include-fixed
 /usr/include/x86_64-linux-gnu
 /usr/include
 ;/home/czh/Advanced_Programming_in_the_Unix_Environment/apue.3e/include"
     )
  )





;------------------------------
;;   CEDET好像已经集成版本2.0了
;---------------------------------------
;(add-to-list 'load-path "~/.emacs.d/cedet-1.1/common")
;(load-file "/home/czh/.emacs.d/cedet-1.1/common/cedet.el") 
;(global-ede-mode 1)                      ; Enable the Project management system
;(semantic-load-enable-code-helpers)      ; Enable prototype help and smart completion 
;(global-srecode-minor-mode 1)            ; Enable template insertion menu
;(global-set-key[(C-f4)] 'speedbar-get-focus) ;speedbar 快捷键
;(define-key c-mode-base-map [(control tab)] 'semantic-ia-complete-symbol-menu) ;自动补全



;--------------------
;  代码消息，配置后可以马上显示出函数的消息
;--------------
(global-semantic-idle-summary-mode 1)

;-------------------
;;启动代码折叠
;-----------------
(add-hook 'c-mode-common-hook   'hs-minor-mode)

;-------------------
;;回车自动缩进、空格显示等的配置
;-----------------

(global-set-key (kbd "RET") 'newline-and-indent)  ; automatically indent when press RET

;; activate whitespace-mode to view all whitespace characters
(global-set-key (kbd "C-c w") 'whitespace-mode)

;; show unncessary whitespace that can mess up your diff
(add-hook 'prog-mode-hook (lambda () (interactive) (setq show-trailing-whitespace 1)))

;; use space to indent by default
(setq-default indent-tabs-mode nil)

;; set appearance of a tab that is represented by 4 spaces
(setq-default tab-width 4)

;下面三个安装包都是与空白键的处理相关的

;-----------------------
;; Package: clean-aindent-mode
;-----------------------

(require 'clean-aindent-mode)
(add-hook 'prog-mode-hook 'clean-aindent-mode)

;---------------------------
;; Package: dtrt-indent
;--------------------------

(require 'dtrt-indent)
(dtrt-indent-mode 1)
(setq dtrt-indent-verbosity 0)

;---------------------
;; Package: ws-butler
;--------------------
(require 'ws-butler)
(add-hook 'c-mode-common-hook 'ws-butler-mode)


;-------------------
;编译相关设置
;--------------------
(global-set-key (kbd "<f5>") (lambda ()
                              (interactive)
                              (setq-local compilation-read-command nil)
                              (call-interactively 'compile)))

;----------------------
;;GDB相关设置
;---------------------
(setq
 ;; use gdb-many-windows by default
 gdb-many-windows t
 ;; Non-nil means display source file containing the main routine at startup
 gdb-show-main t
 )

;----------------------
;;高亮显示 相关设置
;---------------------

(autoload 'idle-highlight-mode "idle-highlight-mode" "highlight the word the point is on" t)
(add-hook 'find-file-hook 'idle-highlight-mode)
(add-hook 'prog-mode-hook 'idle-highlight-mode)

;------------------
;;优化代码注释
;------------------
(defun qiang-comment-dwim-line (&optional arg)

 (interactive "*P")
 (comment-normalize-vars)
 (if (and (not (region-active-p)) (not (looking-at "[ \t]*$")))
     (comment-or-uncomment-region (line-beginning-position) (line-end-position))
     (comment-dwim arg)))

 (global-set-key "\M-;" 'qiang-comment-dwim-line)

;------------------------
;;set transparent effect 透明效果
;------------------------

 (global-set-key [(f12)] 'loop-alpha)
 (setq alpha-list '((100 100) (95 65) (85 55) (75 45) (65 35)))
  (defun loop-alpha ()
  (interactive)
  (let ((h (car alpha-list)))         ;; head value will set to
    ((lambda (a ab)
    (set-frame-parameter (selected-frame) 'alpha (list a ab))
    (add-to-list 'default-frame-alist (cons 'alpha (list a ab)))
        ) (car h) (car (cdr h)))
     (setq alpha-list (cdr (append alpha-list (list h))))
     )
 )



;----------------------
;;参照网上的一些设置
;----------------------
(global-set-key [f4] 'other-window)  ;; 跳转到 Emacs 的另一个buffer窗口

;(defun open-shell-other-buffer ()
;"Open shell in other buffer"
;(interactive)
;(split-window-vertically)
;(shell))
;(global-set-key [(f8)] 'open-shell-other-buffer)
;(global-set-key [C-f8] 'shell)
;;目的是开一个shell的小buffer，用于更方便地测试程序(也就是运行程序了)，我经常会用到。
;;f8就是另开一个buffer然后打开shell，C-f8则是在当前的buffer打开shell
(global-set-key [f8] 'shell-command)



;; ;; ;-------------------
;; ;; ;;  pymacs的配置
;; ;; ;-------------------

;; ;; (autoload 'pymacs-apply "pymacs")
;; ;; (autoload 'pymacs-call "pymacs")
;; ;; (autoload 'pymacs-eval "pymacs" nil t)
;; ;; (autoload 'pymacs-exec "pymacs" nil t)
;; ;; (autoload 'pymacs-load "pymacs" nil t)

;; ;; ;-------------------
;; ;; ;; python complete
;; ;; ;-------------------
;; ;; (require 'pycomplete)
;; ;; (setq auto-mode-alist (cons '("\\.py$" . python-mode) auto-mode-alist))
;; ;; (autoload 'python-mode "python-mode" "Python editing mode." t)
;; ;; (setq interpreter-mode-alist(cons '("python" . python-mode)
;; ;;                           interpreter-mode-alist))

;; ;; python-mode settings
;; (setq auto-mode-alist (cons '("\\.py$" . python-mode) auto-mode-alist))
;; (setq interpreter-mode-alist(cons '("python" . python-mode)
;;                              interpreter-mode-alist))
;; ;; path to python interpreter, e.g.: ~rw/python27/bin/python2.7
;; (setq py-python-command "python")
;; (autoload 'python-mode "python-mode" "Python editing mode." t)

;; ;; pymacs settings
;; (setq pymacs-python-command py-python-command)
;; (autoload 'pymacs-load "pymacs" nil t)
;; (autoload 'pymacs-eval "pymacs" nil t)
;; (autoload 'pymacs-exec "pymacs" nil t)
;; (autoload 'pymacs-apply "pymacs")
;; (autoload 'pymacs-call "pymacs")


;; ;; (require 'pycomplete)

;-----------------------------------
;;linux python ide 打造 
;------------------------------------

;; (package-initialize)
(add-to-list 'exec-path "~/.local/bin")
(add-to-list 'load-path "/home/harlan/.emacs.d/elpa/pyvenv-20160527.442")
(require 'pyvenv)
(elpy-enable)

;;(when (require 'flycheck nil t)
;;  (setq elpy-modules (delq 'elpy-module-flymake elpy-modules))
;;  (add-hook 'elpy-mode-hook 'flycheck-mode))

(require 'py-autopep8)
(add-hook 'elpy-mode-hook 'py-autopep8-enable-on-save)



(setq auto-mode-alist (cons '("\\.py$" . python-mode) auto-mode-alist))
;;(elpy-use-ipython)  ;;无论何种形式的调用ipython，加载python mode时会挂掉

;-----------------------------------
;;  linux golang ide
;----------------------------------------

(add-to-list 'load-path "/home/harlan/.emacs.d/go-mode.el-master")
(require 'go-mode-autoloads)

;;(setenv "GOPATH" "/home/harlan/go")


;;下面两个十分重要，否则emacs找不到go运行的程序
;;(setq exec-path (cons "/usr/local/go/bin" exec-path))  ;;估计也可以去掉，搜索系统的PATH即可了
(add-to-list 'exec-path "/home/harlan/go/bin")
;;保存文件的时候对该源文件做一下gofmt
;(add-hook 'before-save-hook 'gofmt-before-save) ;;下面的代码有包括hook功能了，故这个设置可以屏蔽掉

(defun my-go-mode-hook ()
  ; Call Gofmt before saving
  (add-hook 'before-save-hook 'gofmt-before-save)
  ; Customize compile command to run go build
  (if (not (string-match "go" compile-command))
      (set (make-local-variable 'compile-command)
           "go generate && go build -v && go test -v && go vet"))
  ; Godef jump key binding
  (local-set-key (kbd "M-.") 'godef-jump))
(add-hook 'go-mode-hook 'my-go-mode-hook)

(require 'go-autocomplete)
(require 'auto-complete-config)
(ac-config-default)


