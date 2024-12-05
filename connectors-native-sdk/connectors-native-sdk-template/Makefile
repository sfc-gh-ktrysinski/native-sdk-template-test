CONNECTION=native_sdk_connection
VERSION='"1_0"'

# ***********
#  CORE FLOW
# ***********

.PHONY: copy_internal_components
copy_internal_components:
	./gradlew copyInternalComponents

.PHONY: copy_sdk_components
copy_sdk_components:
	./gradlew copySdkComponents

# ****************************************
#  CREATE INSTANCE FROM VERSION DIRECTORY
# ****************************************

.PHONY: complex_create_app_instance_from_version_dir
complex_create_app_instance_from_version_dir:
	make copy_internal_components
	make copy_sdk_components
	snow app run --connection=$(CONNECTION)

# **********************************
#  CREATE INSTANCE FROM APP VERSION
# **********************************

.PHONY: create_new_version
create_new_version:
	snow app version create $(VERSION) --connection=$(CONNECTION)

.PHONY: create_app_instance_from_app_version
create_app_instance_from_app_version:
	snow app version create $(VERSION) --connection=$(CONNECTION)
	snow app run --version $(VERSION) --connection=$(CONNECTION)

.PHONY: complex_create_app_instance_from_app_version
complex_create_app_instance_from_app_version:
	make copy_internal_components
	make copy_sdk_components
	make create_app_instance_from_app_version

# ******************
#  ADDITIONAL TASKS
# ******************

.PHONY: drop_application
drop_application:
	snow app teardown --connection=$(CONNECTION) --cascade --force

.PHONY: reinstall_application_from_version_dir
reinstall_application_from_version_dir:
	make drop_application
	make complex_create_app_instance_from_version_dir

.PHONY: reinstall_application_from_app_version
reinstall_application_from_app_version:
	make drop_application
	make complex_create_app_instance_from_app_version

.PHONY: update_app_instance
update_app_instance:
	snow app deploy --connection=$(CONNECTION)
