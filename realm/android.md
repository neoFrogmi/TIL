Realm
=====

It is know that Android Realm version is lower that iOS version. Because of this, a lot of issues are present at the moment.

Issue: **Android Low Level heap can be consumed entirely by Realm**:
Realm is an implementation based on a C and C++ as a JNI, plus a Java implementation to use this API. The C and C++ imlementation uses the native heap and the Java implementation uses the Java Heap.
The problem recently solved is the 100% consuming of native heap when many Realm IO operations are executed per second described by the following error.

```
 Build: samsung/degaswifixx/degaswifi:4.4.2/KOT49H/T230XXU0ANJ4:user/release-keys
 Hardware: PXA1088
 Revision: 3
 Bootloader: T230XXU0ANJ4
 Radio: unknown
 Kernel: Linux version 3.10.0-3095390 (dpi@SWDD5701) (gcc version 4.7 (GCC) ) #2 SMP PREEMPT Sat Oct 25 17:37:16 KST 2014

 *** *** *** *** *** *** *** *** *** *** *** *** *** *** *** ***
 Build fingerprint: 'samsung/degaswifixx/degaswifi:4.4.2/KOT49H/T230XXU0ANJ4:user/release-keys'
 Revision: '3'
 pid: 2096, tid: 2096, name: piral.neofrogmi  >>> com.inzpiral.neofrogmi <<<
 signal 11 (SIGSEGV), code 1 (SEGV_MAPERR), fault addr 2d6e7461
     r0 2d6e7461  r1 00000000  r2 77d94d28  r3 77d94d28
     r4 00000000  r5 7d2f89b8  r6 7d19fd00  r7 00000000
     r8 77d94e18  r9 77d94d28  sl 415e7e08  fp bee823fc
     ip 4c2d7365  sp bee82348  lr 00000010  pc 77d5a6b0  cpsr 40030030
...
...
...
 processName:com.inzpiral.neofrogmi
 broadcastEvent : com.inzpiral.neofrogmi SYSTEM_TOMBSTONE
```

This issue was happened on ExecutionView when a lot of IO operations are carried out using saveQuestions() method. **To solve this**, I've refactored some code that allow the code be more efficient and faster to be executed. This enhancement allows ExecutionView carry out less Realm IO operations and therefore, a better way to use the Native Heap.

**In conclusion: ** to prevent the previous error, you must reduce the IO Realm operations per second and prefer use beginTransaction() - commitTransaction() with a lot of IO operations, instead use a beginTransaction() - commitTransaction() per operation.
