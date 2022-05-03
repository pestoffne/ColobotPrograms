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

all: $(PROGRAM_DIR)/lib_list_int.cbot $(PROGRAM_DIR)/lib_list_goal.cbot $(PROGRAM_DIR)/lib_list_object.cbot $(PROGRAM_DIR)/lib_list_upo.cbot \
	$(PROGRAM_DIR)/lib_list_pathpart.cbot $(PROGRAM_DIR)/lib_tree_ilp.cbot $(PROGRAM_DIR)/lib_tree_ii.cbot

$(PROGRAM_DIR)/lib_list_int.cbot: lib_list_template.cbot
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_int.cbot,int,Int,0,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_goal.cbot: lib_list_template.cbot
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_goal.cbot,Goal,Goal,null,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_point.cbot: lib_list_template.cbot
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_point.cbot,point,Point,new point(400, 400),lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_object.cbot: lib_list_template.cbot
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_object.cbot,object,Object,null,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_upo.cbot: lib_list_template.cbot
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_upo.cbot,UnaryPredicateObject,UnaryPredicateObject,null,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_pathpart.cbot: lib_list_template.cbot
	$(call generate_from_template,$(PROGRAM_DIR)/lib_list_pathpart.cbot,PathPart,PathPart,null,lib_list_template.cbot)

$(PROGRAN_DIR)/lib_tree_ilp.cbot: lib_sorted_tree_template.cbot $(PROGRAM_DIR)/lib_list_point.cbot
	$(call generate_sorted_tree,$(PROGRAM_DIR)/lib_tree_ilp.cbot,int,ListPoint,Int,ListPoint,0,null,((X)-(Y)),lib_sorted_tree_template.cbot)

$(PROGRAN_DIR)/lib_tree_ii.cbot: lib_sorted_tree_template.cbot
	$(call generate_sorted_tree,$(PROGRAM_DIR)/lib_tree_ii.cbot,int,int,Int,Int,0,0,((X)-(Y)),lib_sorted_tree_template.cbot)
