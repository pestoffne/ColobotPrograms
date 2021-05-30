PROGRAM_DIR=../program

define generate_from_template
	echo '// This file is generated automaticaly from template. Do not edit.' > $(1)
	cpp -D='TYPE $(2)' -D='TEMPLATE(CLASS) CLASS ## $(3)' -D='NULL $(4)' $(5) |\
		grep -v '^#' | awk '{$$1=$$1};1' >> $(1)

endef

all: $(PROGRAM_DIR)/lib_list_int.txt $(PROGRAM_DIR)/lib_list_goal.txt $(PROGRAM_DIR)/lib_list_point.txt

$(PROGRAM_DIR)/lib_list_int.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_int.txt,int,Int,0,lib_list_template.txt)

$(PROGRAM_DIR)/lib_list_goal.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_goal.txt,Goal,Goal,null,lib_list_template.txt)

$(PROGRAM_DIR)/lib_list_point.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_point.txt,point,Point,new point(400, 400),lib_list_template.txt)
