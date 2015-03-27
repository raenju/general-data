global _start

section .bss

	str: resb 12
	cnt: resb 1
	cnt2: resb 1
	count: resd 1

section .text



_start:
	
	mov eax, 1234
	mov [count], eax
	xor edx, edx
	mov eax, [count]
	mov ebx, 10
	
	mov eax, [count]
	jmp int2str
	
	print:
	mov eax, 4
	mov ebx, 1
	mov ecx, str
	mov edx, [cnt]
	add edx, 2
	int 0x80
	
	mov eax, 1
	mov ebx, 0
	int 0x80
	
	int2str:		;salva o valor de eax em str
	
	push rbp
	mov rbp, rsp
	
	mov ebx, 0
	mov [cnt], ebx
	
	subrot:
	xor rdx, rdx
	mov ebx, 10
	div ebx
	push rdx
	mov edx, [cnt]
	add edx, 1
	mov [cnt], edx
	cmp eax, 0
	
	jg subrot
	mov ebx, [cnt]
	xor ebx, ebx
	build:
	xor rcx, rcx
	pop rcx
	add ecx, '0'
	;xor ebx, ebx
	;mov ebx, [cnt2]
	;mov ecx, 0xa
	mov [str+ebx], ecx
	inc ebx
	;mov [cnt2], ebx
	cmp [cnt], ebx
	
	jg build
	mov ecx, 0xa
	mov ebx, [cnt]
	mov [str+ebx], ecx
	mov ecx, 0
	mov [str+ebx+1], ecx
	pop rbp
	jmp print
	
	
	
	
	
	
section .data

;count: dd 92
