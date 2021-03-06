sbin_PROGRAMS = nft

CLEANFILES = scanner.c parser_bison.c

AM_CPPFLAGS = -I$(top_srcdir)/include
AM_CPPFLAGS += -DDEFAULT_INCLUDE_PATH="\"${sysconfdir}\"" \
		${LIBMNL_CFLAGS} ${LIBNFTNL_CFLAGS}
if BUILD_DEBUG
AM_CPPFLAGS += -g -DDEBUG
endif
if BUILD_XTABLES
AM_CPPFLAGS += ${XTABLES_CFLAGS}
endif

AM_CFLAGS = -Wall								\
	    -Wstrict-prototypes -Wmissing-prototypes -Wmissing-declarations	\
	    -Wdeclaration-after-statement -Wsign-compare -Winit-self		\
	    -Wformat-nonliteral -Wformat-security -Wmissing-format-attribute	\
	    -Wcast-align -Wundef -Wbad-function-cast
	    -Waggregate-return -Wunused -Wwrite-strings


AM_YFLAGS = -d

# yacc and lex generate dirty code
parser_bison.o scanner.o: AM_CFLAGS += -Wno-missing-prototypes -Wno-missing-declarations -Wno-implicit-function-declaration -Wno-nested-externs -Wno-undef -Wno-redundant-decls

BUILT_SOURCES = parser_bison.h

lib_LTLIBRARIES = libnftables.la

libnftables_la_SOURCES =	rule.c				\
		statement.c			\
		datatype.c			\
		expression.c			\
		evaluate.c			\
		proto.c				\
		payload.c			\
		exthdr.c			\
		meta.c				\
		ct.c				\
		netlink.c			\
		netlink_linearize.c		\
		netlink_delinearize.c		\
		segtree.c			\
		rbtree.c			\
		gmputil.c			\
		utils.c				\
		erec.c				\
		mnl.c				\
		iface.c				\
		libnftables.c			\
		scanner.l			\
		parser_bison.y

if BUILD_MINIGMP
mini-gmp.o: AM_CFLAGS += -Wno-sign-compare

libnftables_la_SOURCES +=	mini-gmp.c
endif

nft_SOURCES = main.c

if BUILD_CLI
nft_SOURCES +=	cli.c
endif

libnftables_la_LIBADD	= ${LIBMNL_LIBS} ${LIBNFTNL_LIBS}

if BUILD_XTABLES
libnftables_la_SOURCES  +=	xt.c
libnftables_la_LIBADD   +=  ${XTABLES_LIBS}
endif

nft_LDADD		= libnftables.la
