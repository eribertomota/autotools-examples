
if PYTHON_ENABLED

pythondir = $(PYTHON_SITE_LIB)/acix

nobase_python_PYTHON = __init__.py \
                       core/__init__.py \
                       core/bitvector.py \
                       core/bloomfilter.py \
                       core/cacheclient.py \
                       core/hashes.py \
                       core/indexclient.py \
                       core/ssl.py \
                       scanner/__init__.py \
                       scanner/cache.py \
                       scanner/cacheresource.py \
                       scanner/cachesetup.py \
                       scanner/pscan.py \
                       indexserver/__init__.py \
                       indexserver/index.py \
                       indexserver/indexresource.py \
                       indexserver/indexsetup.py

SUBDIRS = core scanner indexserver
DIST_SUBDIRS = core scanner indexserver

endif
