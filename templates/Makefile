PROGRAM_DIR=../program

$(PROGRAM_DIR)/lib_list_int.txt: lib_list_template.txt
	echo '// This file is generated automaticaly from template. Do not edit.' > $(PROGRAM_DIR)/lib_list_int.txt
	cpp -D='TYPE int' -D='TEMPLATE(CLASS) CLASS ## Int' -D='NULL 0' lib_list_template.txt |\
		grep -v '^#' | awk '{$$1=$$1};1' >> $(PROGRAM_DIR)/lib_list_int.txt
