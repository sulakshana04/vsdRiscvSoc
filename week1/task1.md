## Task-1: Install & Sanity-Check the RISC-V Toolchain

```
Download the RISC-V toolchain from the following link:
riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
```
## step2:  Extract the Toolchain
```
cd ~/Downloads
tar -xzf riscv-toolchain-rv32imac-x86_64-ubuntu.tar.gz
```

## step3: add the path
```
echo 'export PATH=/home/sulakshana/riscv-toolchain/opt/riscv/bin:$PATH' >> ~/.bashrc
source ~/.bashrc
```

## step4: verify
```
riscv32-unknown-elf-gcc --version
```

```
riscv32-unknown-elf-objdump --version
riscv32-unknown-elf-gdb --version
```
file:///home/sulakshana/Pictures/Screenshots/1a.png![image](https://github.com/user-attachments/assets/dd053c7e-830e-4600-96fd-00c3666d1802)

file:///home/sulakshana/Pictures/Screenshots/1b.png![image](https://github.com/user-attachments/assets/773f2de6-c04a-4d12-a89d-63e655b261c0)



