# pwndbg

wsl 의 pwndbg의 사용법을 정리한 문서입니다.

---

### pwndbg의 다운로드와 실행

---

💡 다음 명령어로 wsl에서 gdb와 pwndbg를 설치합니다. (git이 없다면 git도 설치해야합니다.)

```bash
sudo apt-get install gdb (gdb설치)

git clone https://github.com/pwndbg/pwndbg
cd pwndbg
./setup.sh
(pwngdb설치 세 줄 한 번에 복붙)
```

---

![image.png](/assets/img/HowToUsePwndbg/d2aad04d-bfd7-425e-816e-ef526dd88bc0.png)

<aside>

pwndbg를 실행합니다. pwndbg는 “gdb”명령어로 실행할 수 있습니다.

그리고 “exit”로 중단할 수 있습니다.

</aside>

```bash
usungmagic@leeyounsung:~$ gdb (pwndbg 실핼)

pwndbg> exit (pwndbg 나가기)
```

---

### elf 파일 열기와 실행하기

![image.png](/assets/img/HowToUsePwndbg/image.png)

<aside>

“file ./(파일이름)” 으로 elf을 pwndbg에서 열 수 있습니다. (해당 예시의 파일에는 디버그 심볼이 없습니다.)

</aside>

```bash
file ./filename
```

---

💡 다음 명령어로 elf파일의 실행할 수 있습니다.

```bash
pwndbg> r (run) (열려있는 파일을 실행합니다. 뒤에 프로그램인자를 넣어 실행하는 것도 가능합니다)
pwndbg> b (break) (실행의 중단점을 설정합니다. 뒤에 파일 주소를 넣거나 main을 넣어 그 위치에서 더 이상 파일이 실행되지 않게 합니다 주소의 경우 앞에 *을 붙입니다)
pwndbg> c (coutinue) (break를 풀고 프로그램을 실행합니다.)
pwndbg> entry (프로그램 진입점에서 break)
pwndbg> start (main() 위치에서 break)
pwndbg> n (ni) (next instruction) (명령어를 한 줄씩 실행, 함수가 있다면 넘어갑니다.)
pwndbg> s (si) (step into) (함수가 있다면 함수 내부 명령어를 한 줄씩 실행)
pwndbg> finish (si로 함수에 들어갔다면 바로 종료하고 나올 수 있습니다.)
```

### info

```bash
pwndbg> info
pwndbg> i
```

- info list
    
    ```bash
    **info address -- Describe where symbol SYM is stored.
    info all-registers -- List of all registers and their contents, for selected stack frame.
    info args -- All argument variables of current stack frame or those matching REGEXPs.
    info auto-load -- Print current status of auto-loaded files.
    info auxv -- Display the inferior's auxiliary vector.
    info bookmarks -- Status of user-settable bookmarks.
    info breakpoints, info b -- Status of specified breakpoints (all user-settable breakpoints if no argument).
    info checkpoints -- IDs of currently known checkpoints.
    info classes -- All Objective-C classes, or those matching REGEXP.
    info common -- Print out the values contained in a Fortran COMMON block.
    info connections -- Target connections in use.
    info copying -- Conditions for redistributing copies of GDB.
    info dcache -- Print information on the dcache performance.
    info display -- Expressions to display when program stops, with code numbers.
    info exceptions -- List all Ada exception names.
    info extensions -- All filename extensions associated with a source language.
    info files -- Names of targets and files being debugged.
    info float -- Print the status of the floating point unit.
    info frame, info f -- All about the selected stack frame.
    info frame-filter -- List all registered Python frame-filters.
    info functions -- All function names or those matching REGEXPs.
    info guile, info gu -- Prefix command for Guile info displays.
    info inferiors -- Print a list of inferiors being managed.
    info line -- Core addresses of the code for a source line.
    info locals -- All local variables of current stack frame or those matching REGEXPs.
    info macro -- Show the definition of MACRO, and it's source location.
    info macros -- Show the definitions of all macros at LINESPEC, or the current source location.
    info main -- Get main symbol to identify entry point into program.
    info mem -- Memory region attributes.
    info missing-debug-handlers -- GDB command to list missing debug handlers.
    info module -- Print information about modules.
    info modules -- All module names, or those matching REGEXP.
    info os -- Show OS data ARG.
    info pretty-printer -- GDB command to list all registered pretty-printers.
    info probes -- Show available static probes.
    info proc -- Show additional information about a process.
    info program -- Execution status of the program.
    info record, info rec -- Info record options.
    info registers, info r -- List of integer registers and their contents, for selected stack frame.
    info scope -- List the variables local to a scope.
    info selectors -- All Objective-C selectors, or those matching REGEXP.
    info sharedlibrary, info dll -- Status of loaded shared object libraries.
    info signals, info handle -- What debugger does when program gets various signals.
    info skip -- Display the status of skips.
    info source -- Information about the current source file.
    info sources -- All source files in the program or those matching REGEXP.
    info stack, info s -- Backtrace of the stack, or innermost COUNT frames.
    info static-tracepoint-markers -- List target static tracepoints markers.
    info symbol -- Describe what symbol is at location ADDR.
    info target -- Names of targets and files being debugged.
    info tasks -- Provide information about all known Ada tasks.
    info terminal -- Print inferior's saved terminal status.
    info threads -- Display currently known threads.
    info tracepoints, info tp -- Status of specified tracepoints (all tracepoints if no argument).
    info tvariables -- Status of trace state variables and their values.
    info type-printers -- GDB command to list all registered type-printers.
    info types -- All type names, or those matching REGEXP.
    info unwinder -- GDB command to list unwinders.
    info variables -- All global and static variable names or those matching REGEXPs.
    info vector -- Print the status of the vector unit.
    info vtbl -- Show the virtual function table for a C++ object.
    info warranty -- Various kinds of warranty you do not have.
    info watchpoints -- Status of specified watchpoints (all watchpoints if no argument).
    info win -- List of all displayed windows.
    info xmethod -- GDB command to list registered xmethod matchers.**
    ```
    

<aside>

info는 프로그램의 정보를 알 수 있는 기능입니다. i 또는 info로 그 사용법을 알 수 있습니다.

</aside>

💡 많이 사용하는 info

```bash
pwndbg> i r (info registers) (레지스터의 값을 확인할 때 사용합니다.)
pwndbg> i b (info breakpoints) (breakpoint 확인)
```

### breakpoint

💡 실행 중단점을 설정하는 break point를 보려면 info breakpoint를 사용합니다.

![image.png](/assets/img/HowToUsePwndbg/image%201.png)

```bash
pwndbg> b $rdi (특정 레지스터가 가진 주소값을 breakpoint로 설정)
pwndbg> disable 1 (그 번호의 breakpoint를 비활성화)
pwndbg> enable 1 (그 번호의 breakpoint를 활성화)
pwndbg> d 1 (delete 1) (그 번호의 breakpoint를 삭제)
```

### disassemble

💡 disassemble은 어셈블리 코드를 보여줍니다.

```bash
pwndbg> disass <함수> (disassemble main) (해당 함수가 반환될때까지 디스어셈블)
pwndbg> u (가독성 좋은 디스어셈블 코드 출력)
pwndbg> nearpc
pwndbg> pdisass
```

### examine / telescope/ print

💡 examine은 임의 주소의 값을 볼 수 있는 명령어입니다. (x는 실행 도중에만 사용할 수 있습니다.)

| **포멧** | **크기** |
| --- | --- |
| **x** : 16진수 | b (byte) : 1 byte |
| **o** : 8진수 | h (halfword) : 2 byte |
| **d** : 10진수 | w (word) : 4 byte |
| **u** : :부호 없는 10진수 | g (giant) : 8byte |
| **t** : 2진수 |  |
| **f** : float 형 |  |
| **a** : 주소 |  |
| **i** : 명령어 |  |
| **c** : 문자 |  |
| **s** : 문자열 |  |

💡 telescope는 메모리가 참조하는 주소도 보여줍니다.

```bash
pwndbg> tele $rsp
```

💡레지스터의 값을 직접 볼 때는 print가 더 좋을 수 있습니다. examine은 주소를 통해 해석하기 때문

```bash
pwndbg> p/<형변환> <주소 및 레지스터>
```

```bash
x/는 다음과 같은 형식을 사용

pwndbg> x/<포멧 및 크기> <주소 및 레지스터>
pwndbg> x/<개수><포멧 및 크기> <주소 및 레지스터>
ex) x/10gx %rsp (rsp에서 80바이트 8바이트씩 출력)
```

### 메모리 관련 명령어

💡 vmmap은 가상 메모리의 레이아웃을 보여줍니다.

![image.png](/assets/img/HowToUsePwndbg/image%202.png)

 vmmap의 start 주소 + 디스어셈블러에서 본 주소를 하면 중단점 설정할 때 좋습니다.

```bash
pwndbg> vmmap
```

<aside>

💡어떤 파일을 메모리에 적재하는 것을 매핑이라고 합니다. 메모리 레이아웃에서 

/usr/lib/x86_64-linux-gnu/libc.so.6 이 매핑된 파일들을 의미합니다.

리눅스에서는 ELF를 실행할때 ELF의 코드와 여러 데이터를 기싱 메모리에 매핑하고 해당 ELF애 링크된 **공유 오브젝트(Shared Object, so)** 추가로 메모리에 매핑합니다. 공유 오브젝트는 윈도우의 DLL과 대응되는 개념으로 자주 사용된는 함수들을 미리 컴파일해둔 것입니다.

C언어의 printf(), scanf() 등이 리눅스에서는 Libc에 구현되어있습니다. 공유 오브젝트에 이미 구현된 함수를 호출할 때는 매핑된 메모리에 존재하는 함수를 대신 호출합니다.

</aside>

---

💡 콜 스텍(call stack)은 함수 호출 순서를 저장하는 구조입니다. 콜 스택은 디버깅에서 유용하게 사용될 수 있습니다. 만약 함수에 전달된 인자에 문제가 생겨 버그가 발생하면 콜 스택을 거슬러 올라가 버그의 원인을 찾을  수 있습니다. 이때 backtrace 명령어를 사용할 수 있습니다.

![image.png](/assets/img/HowToUsePwndbg/image%203.png)

![image.png](/assets/img/HowToUsePwndbg/image%204.png)

```bash
pwndbg> bt(backtrace)
```

---

💡 dump memory 는 프로세스 메모리 상태를 파일로 저장할 때 사용하는 명령어입니다. 

![image.png](/assets/img/HowToUsePwndbg/image%205.png)

![image.png](/assets/img/HowToUsePwndbg/image%206.png)

```bash
pwndbg> dump memory <파일이름> <시작주소> <끝주소>
```

<aside>

💡 0x401000부터 0x402000을 code_section이라고 이름붙인 이유는 이 부분에 실행권한이 있기 때문입니다.

</aside>

### context

💡  프로그램을 한 줄씩 실행할 때마다 뜨는 것을 맥락(Context)라고 부릅니다. Context는 ctx라는 단축 명령어를 통해서도 볼 수 있습니다.

![image.png](/assets/img/HowToUsePwndbg/image%207.png)

<aside>

REGISTER 부분은 레지스터의 상태를 보여줍니다.

DISASM 부분은 rip부터 여러 줄에 걸쳐 디스어셈블된 결과를 보여줍니다.

STACK 부분은 rsp 부터 여러 줄에 걸쳐 디스어셈블된 결과를 보여줍니다.

BACKTRACE 부분은 현재 rip에 도달할 때까지 어떤 함수들이 중첩되어 호출되었는지를 보여줍니다.

</aside>

```bash
set context-output /dev/null (context 끄기)

set context-output stdout (context 켜기)
```

### set

💡 set은 메모리의 상태를 변경할 수 있는 명령어입니다. (set을 하고 나선 continue를 해야 유지 run을 하면 처음부터임)

```bash
pwndbg> set <주소 or 레지스터> = <변경할 값>

에시)

pwndbg> set $rax = 0
pwndbg> set $rsp = $rbp

pwndbg> set *(unsinged int*)0x400000 = 10 (0x400000을 unsigned int로 역참조하고 10 저장 int는 4바이트)
pwndbg> set *(float*)0x400010 = 3.14 (0x400010을 float로 역참조하고 3.14 저장 float는 4바이트)
```