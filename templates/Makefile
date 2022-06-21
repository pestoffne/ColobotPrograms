PROGRAM_DIR=../program
INCLUDE_DIR=include
PARTS_DIR=../program/parts

define generate_list
	echo '// Generated file.' > $(1)
	cpp -I$(INCLUDE_DIR) -D='TYPE $(2)' -D='TEMPLATE(CLASS) CLASS ## $(3)' -D='NULL $(4)' -D='EXTERN $(5)' $(6) |\
		grep -v '^#' | awk '{$$1=$$1};1' >> $(1)
endef

define generate_sorted_tree
	echo '// Generated file.' > $(1)
	cpp -I$(INCLUDE_DIR) -D='KEY $(2)' -D='VALUE $(3)' -D='TEMPLATE(CLASS) CLASS ## $(4) ## $(5)' \
	-D='KEY_NULL $(6)' -D='VALUE_NULL $(7)' -D='CMP(X,Y) $(8)' $(9) |\
                grep -v '^#' | awk '{$$1=$$1};1' >> $(1)
endef

define generate_matrix
	echo '// Generated file.' > $(1)
	cpp -I$(INCLUDE_DIR) -D='TYPE $(2)' -D='ZERO $(3)' -D='ONE $(4)' $(5) |\
		grep -v '^#' | awk '{$$1=$$1};1' >> $(1)
endef

define generate_affine
	echo '// Generated file.' > $(1)
	cpp -I$(INCLUDE_DIR) -D='SIZE $(2)' $(3) |\
		grep -v '^#' | awk '{$$1=$$1};1' >> $(1)
endef

define generate_0
	echo '// Generated file.' > $(1)
	cpp -I$(INCLUDE_DIR) $(2) | grep -v '^#' | awk '{$$1=$$1};1' >> $(1)
endef

define assemble_parts
	cpp -I$(PARTS_DIR) $(2) | grep -v '^#' | awk '{$$1=$$1};1' > $(1)
endef

.PHONY: all clean

all: $(PROGRAM_DIR)/lib_list_int.cbot $(PROGRAM_DIR)/lib_list_goal.cbot \
$(PROGRAM_DIR)/lib_list_object.cbot $(PROGRAM_DIR)/lib_list_upo.cbot \
$(PROGRAM_DIR)/lib_tree_ilp.cbot $(PROGRAM_DIR)/lib_tree_ii.cbot \
$(PROGRAM_DIR)/lib_matrix_float.cbot \
$(PROGRAM_DIR)/lib_matrix_float.cbot \
$(PROGRAM_DIR)/lib_affine_coordinate_system_2d.cbot \
$(PROGRAM_DIR)/lib_affine_coordinate_system_3d.cbot \
$(PROGRAM_DIR)/lib_path_all.cbot

clean:
	rm -vf $(PROGRAM_DIR)/lib_list_*.cbot $(PROGRAM_DIR)/lib_tree_*.cbot \
	$(PROGRAM_DIR)/lib_matrix_*.cbot \
	$(PROGRAM_DIR)/lib_affine_coordinate_system_*d.cbot \
	$(PARTS_DIR)/lib_path_arc.cbot \
	$(PARTS_DIR)/lib_path_compiled.cbot \
	$(PARTS_DIR)/lib_path_line.cbot \
	$(PARTS_DIR)/lib_path.cbot \
	$(PROGRAM_DIR)/lib_path_all.cbot

$(PROGRAM_DIR)/lib_list_int.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PROGRAM_DIR)/lib_list_int.cbot,int,Int,0,1,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_goal.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PROGRAM_DIR)/lib_list_goal.cbot,Goal,Goal,null,1,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_point.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PROGRAM_DIR)/lib_list_point.cbot,point,Point,new point(400, 400),1,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_object.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PROGRAM_DIR)/lib_list_object.cbot,object,Object,null,1,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_list_upo.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PROGRAM_DIR)/lib_list_upo.cbot,UnaryPredicateObject,UnaryPredicateObject,null,1,lib_list_template.cbot)

$(PARTS_DIR)/lib_list_path_part.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PARTS_DIR)/lib_list_path_part.cbot,PathPart,PathPart,null,0,lib_list_template.cbot)

$(PARTS_DIR)/lib_list_path_node.cbot: lib_list_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_list,$(PARTS_DIR)/lib_list_path_node.cbot,PathNode,PathNode,null,0,lib_list_template.cbot)

$(PROGRAM_DIR)/lib_tree_ilp.cbot: lib_sorted_tree_template.cbot $(PROGRAM_DIR)/lib_list_point.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_sorted_tree,$(PROGRAM_DIR)/lib_tree_ilp.cbot,int,ListPoint,Int,ListPoint,0,null,((X)-(Y)),lib_sorted_tree_template.cbot)

$(PROGRAM_DIR)/lib_tree_ii.cbot: lib_sorted_tree_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_sorted_tree,$(PROGRAM_DIR)/lib_tree_ii.cbot,int,int,Int,Int,0,0,((X)-(Y)),lib_sorted_tree_template.cbot)

$(PROGRAM_DIR)/lib_matrix_float.cbot: lib_matrix_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_matrix,$(PROGRAM_DIR)/lib_matrix_float.cbot,float,0.0,1.0,lib_matrix_template.cbot)

$(PROGRAM_DIR)/lib_affine_coordinate_system_2d.cbot: lib_affine_coordinate_system_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_affine,$(PROGRAM_DIR)/lib_affine_coordinate_system_2d.cbot,2,lib_affine_coordinate_system_template.cbot)

$(PROGRAM_DIR)/lib_affine_coordinate_system_3d.cbot: lib_affine_coordinate_system_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_affine,$(PROGRAM_DIR)/lib_affine_coordinate_system_3d.cbot,3,lib_affine_coordinate_system_template.cbot)

$(PARTS_DIR)/lib_path_arc.cbot: lib_path_arc_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_0,$(PARTS_DIR)/lib_path_arc.cbot,lib_path_arc_template.cbot)

$(PARTS_DIR)/lib_path_compiled.cbot: lib_path_compiled_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_0,$(PARTS_DIR)/lib_path_compiled.cbot,lib_path_compiled_template.cbot)

$(PARTS_DIR)/lib_path_line.cbot: lib_path_line_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_0,$(PARTS_DIR)/lib_path_line.cbot,lib_path_line_template.cbot)

$(PARTS_DIR)/lib_path.cbot: lib_path_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_0,$(PARTS_DIR)/lib_path.cbot,lib_path_template.cbot)

$(PARTS_DIR)/lib_path_node.cbot: lib_path_node_template.cbot $(INCLUDE_DIR)/macro.cbot
	$(call generate_0,$(PARTS_DIR)/lib_path_node.cbot,lib_path_node_template.cbot)

$(PROGRAM_DIR)/lib_path_all.cbot: lib_path_all_template.cbot \
$(PARTS_DIR)/lib_path_part.cbot $(PARTS_DIR)/lib_list_path_part.cbot \
$(PARTS_DIR)/lib_path_node.cbot $(PARTS_DIR)/lib_list_path_node.cbot \
$(PARTS_DIR)/lib_path_arc.cbot $(PARTS_DIR)/lib_path_line.cbot \
$(PARTS_DIR)/lib_path_compiled.cbot $(PARTS_DIR)/lib_path.cbot
	$(call assemble_parts,$(PROGRAM_DIR)/lib_path_all.cbot,lib_path_all_template.cbot)
