;; source files
(set @m_files     (filelist "^objc/.*.m$"))
(set @nu_files 	  (filelist "^nu/.*nu$"))

(set SYSTEM ((NSString stringWithShellCommand:"uname") chomp))
(case SYSTEM
      ("Darwin"
               (set @cflags "-g -fobjc-gc -std=gnu99 -DDARWIN -I/usr/local/pgsql/include")
               (set @ldflags "-framework Foundation -framework Nu -lpq -L/usr/local/pgsql/lib"))
      ("Linux"
              (set @arch (list "i386"))
              (set @cflags "-g -std=gnu99 -DLINUX -I/usr/include/GNUstep/Headers -I/usr/local/include -I/usr/local/pgsql/include -fconstant-string-class=NSConstantString ")
              (set @ldflags "-L/usr/local/lib -lNu -lpq -L/usr/local/pgsql/lib"))
      (else nil))

;; framework description
(set @framework "NuPostgreSQL")
(set @framework_identifier "nu.programming.nupostgresql")
(set @framework_creator_code "????")

(compilation-tasks)
(framework-tasks)

(task "clobber" => "clean" is
      (SH "rm -rf #{@framework_dir}"))

(task "default" => "framework")

(task "doc" is (SH "nudoc"))

(task "install" => "framework" is
      (SH "sudo rm -rf /Library/Frameworks/#{@framework}.framework")
      (SH "sudo cp -rp #{@framework}.framework /Library/Frameworks/#{@framework}.framework"))

(task "test" => "framework" is
      (SH "nutest test/test_*.nu"))
