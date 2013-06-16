CMAKE_MINIMUM_REQUIRED (VERSION 2.8.7)
PROJECT (cryptopp)

OPTION (CRYPTOPP_BUILD_TESTS "Build cryptopp tests" ON)
OPTION (CRYPTOPP_DISABLE_ASM "Disable ASM" ON)
OPTION (CRYPTOPP_DISABLE_SSSE3 "Disable SSSE3" ON)
OPTION (CRYPTOPP_DISABLE_AESNI "Disable AES-NI" ON)

SET (cryptopp_SOURCES
	3way.cpp
	adler32.cpp
	algebra.cpp
	algparam.cpp
	arc4.cpp
	asn.cpp
	authenc.cpp
	base32.cpp
	base64.cpp
	basecode.cpp
	bfinit.cpp
	blowfish.cpp
	blumshub.cpp
	camellia.cpp
	cast.cpp
	casts.cpp
	cbcmac.cpp
	ccm.cpp
	channels.cpp
	cmac.cpp
	cpu.cpp
	crc.cpp
	cryptlib_bds.cpp
	cryptlib.cpp
	default.cpp
	des.cpp
	dessp.cpp
	dh2.cpp
	dh.cpp
	dll.cpp
	dsa.cpp
	eax.cpp
	ec2n.cpp
	eccrypto.cpp
	ecp.cpp
	elgamal.cpp
	emsa2.cpp
	eprecomp.cpp
	esign.cpp
	files.cpp
	filters.cpp
	fips140.cpp
	fipstest.cpp
	gcm.cpp
	gf2_32.cpp
	gf256.cpp
	gf2n.cpp
	gfpcrypt.cpp
	gost.cpp
	gzip.cpp
	hex.cpp
	hmac.cpp
	hrtimer.cpp
	ida.cpp
	idea.cpp
	integer.cpp
	iterhash.cpp
	luc.cpp
	mars.cpp
	marss.cpp
	md2.cpp
	md4.cpp
	md5.cpp
	misc.cpp
	modes.cpp
	mqueue.cpp
	mqv.cpp
	nbtheory.cpp
	network.cpp
	oaep.cpp
	osrng.cpp
	panama.cpp
	pch.cpp
	pkcspad.cpp
	polynomi.cpp
	pssr.cpp
	pubkey.cpp
	queue.cpp
	rabin.cpp
	randpool.cpp
	rc2.cpp
	rc5.cpp
	rc6.cpp
	rdtables.cpp
	rijndael.cpp
	ripemd.cpp
	rng.cpp
	rsa.cpp
	rw.cpp
	safer.cpp
	salsa.cpp
	seal.cpp
	seed.cpp
	serpent.cpp
	sha3.cpp
	shacal2.cpp
	sha.cpp
	sharkbox.cpp
	shark.cpp
	simple.cpp
	skipjack.cpp
	socketft.cpp
	sosemanuk.cpp
	square.cpp
	squaretb.cpp
	strciphr.cpp
	tea.cpp
	tftables.cpp
	tiger.cpp
	tigertab.cpp
	trdlocal.cpp
	ttmac.cpp
	twofish.cpp
	vmac.cpp
	wait.cpp
	wake.cpp
	whrlpool.cpp
	winpipes.cpp
	xtr.cpp
	xtrcrypt.cpp
	zdeflate.cpp
	zinflate.cpp
	zlib.cpp
)

SET (cryptopp_HEADERS
	3way.h
	adler32.h
	aes.h
	algebra.h
	algparam.h
	arc4.h
	argnames.h
	asn.h
	authenc.h
	base32.h
	base64.h
	basecode.h
	bench.h
	blowfish.h
	blumshub.h
	camellia.h
	cast.h
	cbcmac.h
	ccm.h
	channels.h
	cmac.h
	config.h
	cpu.h
	crc.h
	cryptlib.h
	default.h
	des.h
	dh2.h
	dh.h
	dll.h
	dmac.h
	dsa.h
	eax.h
	ec2n.h
	eccrypto.h
	ecp.h
	elgamal.h
	emsa2.h
	eprecomp.h
	esign.h
	factory.h
	files.h
	filters.h
	fips140.h
	fltrimpl.h
	gcm.h
	gf2_32.h
	gf256.h
	gf2n.h
	gfpcrypt.h
	gost.h
	gzip.h
	hex.h
	hmac.h
	hrtimer.h
	ida.h
	idea.h
	integer.h
	iterhash.h
	lubyrack.h
	luc.h
	mars.h
	md2.h
	md4.h
	md5.h
	mdc.h
	misc.h
	modarith.h
	modes.h
	modexppc.h
	mqueue.h
	mqv.h
	nbtheory.h
	network.h
	nr.h
	oaep.h
	oids.h
	osrng.h
	panama.h
	pch.h
	pkcspad.h
	polynomi.h
	pssr.h
	pubkey.h
	pwdbased.h
	queue.h
	rabin.h
	randpool.h
	rc2.h
	rc5.h
	rc6.h
	resource.h
	rijndael.h
	ripemd.h
	rng.h
	rsa.h
	rw.h
	safer.h
	salsa.h
	seal.h
	secblock.h
	seckey.h
	seed.h
	serpent.h
	serpentp.h
	sha3.h
	shacal2.h
	sha.h
	shark.h
	simple.h
	skipjack.h
	smartptr.h
	socketft.h
	sosemanuk.h
	square.h
	stdcpp.h
	strciphr.h
	tea.h
	tiger.h
	trdlocal.h
	trunhash.h
	ttmac.h
	twofish.h
	validate.h
	vmac.h
	wait.h
	wake.h
	whrlpool.h
	winpipes.h
	words.h
	xtrcrypt.h
	xtr.h
	zdeflate.h
	zinflate.h
	zlib.h
)

INCLUDE_DIRECTORIES (${CMAKE_CURRENT_SOURCE_DIR})

# Set flags
IF (CRYPTOPP_DISABLE_ASM)
	ADD_DEFINITIONS (-DCRYPTOPP_DISABLE_ASM)
ENDIF ()
IF (CRYPTOPP_DISABLE_SSSE3)
	ADD_DEFINITIONS (-DCRYPTOPP_DISABLE_SSSE3)
ENDIF ()
IF (CRYPTOPP_DISABLE_AESNI)
	ADD_DEFINITIONS (-DCRYPTOPP_DISABLE_AESNI)
ENDIF ()

ADD_LIBRARY (cryptopp
	${cryptopp_SOURCES}
	${cryptopp_HEADERS}
)

IF (CRYPTOPP_BUILD_TESTS)
	ENABLE_TESTING ()
	# Generate your adhoc.cpp.proto
	SET (cryptopp_TEST_SOURCES
		bench.cpp
		bench2.cpp
		test.cpp
		validat1.cpp
		validat2.cpp
		validat3.cpp
		datatest.cpp
		regtest.cpp
		fipsalgt.cpp
		dlltest.cpp)
	ADD_CUSTOM_COMMAND (
		OUTPUT adhoc.cpp
		COMMAND ${CMAKE_COMMAND} -E copy ${CMAKE_CURRENT_SOURCE_DIR}/adhoc.cpp.proto ${CMAKE_CURRENT_BINARY_DIR}/adhoc.cpp
	)
	LIST (APPEND cryptopp_TEST_SOURCES
		adhoc.cpp
	)
	ADD_EXECUTABLE (cryptest
		${cryptopp_TEST_SOURCES}
	)
	TARGET_LINK_LIBRARIES (cryptest
		cryptopp)
	# Run validation tests
	ADD_TEST (NAME cryptopp_validation_tests
		COMMAND ${CMAKE_COMMAND} -E chdir ${CMAKE_CURRENT_SOURCE_DIR} $<TARGET_FILE:cryptest> v)
	# Run test scripts
	ADD_TEST (NAME cryptopp_test_scripts
		COMMAND ${CMAKE_COMMAND} -E chdir ${CMAKE_CURRENT_SOURCE_DIR} $<TARGET_FILE:cryptest> tv TestVectors/all.txt)
ENDIF ()