
all: gen compile disass spike

gen: clean
	@echo '[UpTickPro] Test Generation ------'
	aapg setup
	aapg gen --config_file $(PWD)/rv32i.yaml --asm_name test --output_dir $(PWD) --arch rv64

compile:
	@echo '[UpTickPro] Test Compilation ------'
	riscv32-unknown-elf-gcc -march=rv64im -mabi=lp64 -static -mcmodel=medany -fvisibility=hidden -nostdlib -nostartfiles -I$(PWD)/work/common -T$(PWD)/test.ld test.S $(PWD)/work/common/crt.S -o test.elf

disass: compile
	@echo '[UpTickPro] Test Disassembly ------'
	riscv32-unknown-elf-objdump -D test.elf > test.disass

spike: compile
	@echo '[UpTickPro] Spike Run ------'
	spike --isa=rv64im test.elf 
	spike --log-commits --log  test_spike.dump --isa=rv64im +signature=test_spike_signature.log test.elf

clean:
	@echo '[UpTickPro] Clean ------'
	rm -rf work *.elf *.disass *.log *.dump *.ld *.S *.ini
