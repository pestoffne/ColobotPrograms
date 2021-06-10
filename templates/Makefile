PROGRAM_DIR=../program

define generate_from_template
	echo '// This file is generated automaticaly from template. Do not edit.' > $(1)
	cpp -D='TYPE $(2)' -D='TEMPLATE(CLASS) CLASS ## $(3)' -D='NULL $(4)' $(5) |\
		grep -v '^#' | awk '{$$1=$$1};1' >> $(1)

endef

define generate_sorted_tree
	echo '// This file is generated automaticaly from template. Do not edit.' > $(1)
	cpp -D='KEY $(2)' -D='VALUE $(3)' -D='TEMPLATE(CLASS) CLASS ## $(4) ## $(5)' -D='KEY_NULL $(6)' -D='VALUE_NULL $(7)' -D='CMP(X,Y) $(8)' $(9) |\
                grep -v '^#' | awk '{$$1=$$1};1' >> $(1)
endef

all: $(PROGRAM_DIR)/lib_list_int.txt $(PROGRAM_DIR)/lib_list_goal.txt $(PROGRAM_DIR)/lib_list_object.txt $(PROGRAM_DIR)/lib_list_upo.txt \
	$(PROGRAN_DIR)/lib_tree_ilp.txt $(PROGRAN_DIR)/lib_tree_ii.txt

$(PROGRAM_DIR)/lib_list_int.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_int.txt,int,Int,0,lib_list_template.txt)

$(PROGRAM_DIR)/lib_list_goal.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_goal.txt,Goal,Goal,null,lib_list_template.txt)

$(PROGRAM_DIR)/lib_list_point.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_point.txt,point,Point,new point(400, 400),lib_list_template.txt)

$(PROGRAM_DIR)/lib_list_object.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_object.txt,object,Object,null,lib_list_template.txt)

$(PROGRAM_DIR)/lib_list_upo.txt: lib_list_template.txt
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_upo.txt,UnaryPredicateObject,UnaryPredicateObject,null,lib_list_template.txt)

$(PROGRAN_DIR)/lib_tree_ilp.txt: lib_sorted_tree_template.txt $(PROGRAM_DIR)/lib_list_point.txt
	$(call generate_sorted_tree,$(PROGRAM_DIR)/lib_tree_ilp.txt,int,ListPoint,Int,ListPoint,0,null,((X)-(Y)),lib_sorted_tree_template.txt)

$(PROGRAN_DIR)/lib_tree_ii.txt: lib_sorted_tree_template.txt
	$(call generate_sorted_tree,$(PROGRAM_DIR)/lib_tree_ii.txt,int,int,Int,Int,0,0,((X)-(Y)),lib_sorted_tree_template.txt)
