컴퓨터의 개념 및 실습
===

이 날 이전 노트는 에버노트에 작성해놈.. 에버노트 전에는 원노트에 작성해놈... (자꾸 뭐가 나은지 고민)

<p align=right>20170327</p>

청문회 1시간째 진행 중... 겨수님,, 저희 진도 언제나가요

수업 시간에는 언제든지 질문을 하세요

15시 34분 드디어 진도를 나간다 (수업은 14시 30분부터 시작)

instruction set architecture에는 기본적으로 memory가 있고, resister set이 있고, instruction set이 있다.

ISA의 documentation을 들여다보면 이런 것들이 다 나와있다

레지스터는 일단 8개가 있고, 프로그램 카운터가 있고, 컨디션 코드가 있고

컨디션 코드는 뒤에 나오지만 간단히 설명하면 마지막으로 계산된 값이 0이었느냐 음수였느냐 양수였느냐를 저장하는 3개의 플립플롭. Z, P, N 셋 중 하나가 set이 된다.

opcode는 기본적으로 3개의 분류

- 작업 (더하기 등)
- 데이터 이동
- 컨트롤(점프 등)

작업 operate instruction에는 ADD, AND, NOT 세 개 밖에 없다

- NOT 1001 Dst Src 111 111
- ADD (Register) 0001 Dst Src1 0 00 Src2
- AND (Register) 0101 Dst Src1 0 00 Src2
- ADD (Immediate) 0001 Dst Src1 1 Imm5
- AND (Immediate) 0101 Dst Src1 1 Imm5
 - *Note: Immediate field is sign-extended*

Date Movement Instruction

load 인스트럭션에만 3개가 있음

-> 다 주소값을 지정하는 방법이 다르다

- LD, ST: 현재 PC 기준으로 메모리 주소 지칭
	- LD 0010 Dst PCoffset9
	- ST 0011 Src PCoffset9
- LDI, STI: PC-relative로 주소값을 지정하면, 그 지정된 주소값에 있는 값에 해당하는 주소를 지칭
	- LDI 1010 Dst PCoffset9
	- STI 1011 Src PCoffset9
- LDR, STR: base에 해당하는 레지스터의 값을 주소값으로
	- LDR 0110 Dst Base offset6
	- STR 0111 Src Base offset6
- Load Effective Address?
	- PC-relative 처럼 주소값을 계산해서 그 계산된 주소값을 레지스터에 집어넣는다
	- LEA 1110 Dst PCoffset9

이제 여러분이 필히 가지고 다녀야 하는 것... 책 525페이지에 해당하는 LC-5 Instruction Set

가장 일반적인 내용이 LDR, STR, 레지스터의 값으로 지정하는 것

앞으로는 conditional한 주소값 지정을 할 것 -> 그것이 컨트롤 인스트럭션..?

그게 있어야 더 하이레벨 구현을 할 수 있다

그걸 다음시간에 배울 것

TRAP: OS와의 연결 경로라고 생각. PC를 OS의 서비스 루틴 어쩌구에 가져다 놓고 끝나면 다시 돌아온다

Condition Codes: 7개의 인스트럭션은 컨디션 코드가 나온다 (ADD, AND, NOT, LD, LDR, LDI, LEA)

쓰여지는 값이 양수면 P, 음수면 N, 0이면 Z가 1이 되고, 동시에 2개 이상이 1이 될 수는 없다.

Branch Instruction: 컨디션코드가 설정한 값과 맞으면 PC-relative하게 점프, 아니면 다음 인스트럭션 실행

- BR 0000 n z p PCoffset9

챕터05 29번 슬라이드의 x3006번 인스트럭션에 오타 (책 134쪽 참조)

0001011011000001 -> 0001011011000100

- TRAP: 운영체제와 소통
	- 1111 0000 trapvect8
	- vector
		- x23: 키보드에서 한글자를 가져와 R0에 넣는다
		- x21: R0에서 한글자를 모니터로 보낸다
		- x25: 프로그램을 멈춘다

~~ LC-3에서 클럭마다 데이터가 어떻게 넘어가는지에 대한 설명 ~~

현재시각 16시 30분.. 겨수님 저희 언제 끝나요

다음 수업 있다는 친구의 발언으로 끝난다!!
