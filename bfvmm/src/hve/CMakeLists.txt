#
# Copyright (C) 2019 Assured Information Security, Inc.
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in all
# copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

if(${BUILD_TARGET_ARCH} STREQUAL "x86_64")
    list(APPEND SOURCES
        arch/intel_x64/apic/x2apic.cpp
        arch/intel_x64/pci/pci_configuration_space.cpp
        arch/intel_x64/vmexit/cpuid.cpp
        arch/intel_x64/vmexit/external_interrupt.cpp
        arch/intel_x64/vmexit/io_instruction.cpp
        arch/intel_x64/vmexit/msr.cpp
        arch/intel_x64/vmexit/vmcall.cpp
        arch/intel_x64/vmexit/yield.cpp
        arch/intel_x64/vmcall/domain_op.cpp
        arch/intel_x64/vmcall/run_op.cpp
        arch/intel_x64/vmcall/vcpu_op.cpp
        arch/intel_x64/domain.cpp
        arch/intel_x64/uart.cpp
        arch/intel_x64/vcpu.cpp
    )

elseif(${BUILD_TARGET_ARCH} STREQUAL "aarch64")
    message(WARNING "Unimplemented")
else()
    message(FATAL_ERROR "Unsupported architecture")
endif()

add_shared_library(
    boxy_hve
    SOURCES ${SOURCES}
    DEFINES SHARED_BOXY_HVE
    DEFINES SHARED_EAPIS_HVE
    DEFINES SHARED_HVE
    DEFINES SHARED_MEMORY_MANAGER
    DEFINES SHARED_INTRINSICS
)

add_static_library(
    boxy_hve
    SOURCES ${SOURCES}
    DEFINES STATIC_BOXY_HVE
    DEFINES STATIC_EAPIS_HVE
    DEFINES STATIC_HVE
    DEFINES STATIC_MEMORY_MANAGER
    DEFINES STATIC_INTRINSICS
)