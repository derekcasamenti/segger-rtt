project('segger-rtt', 'c',
    version : '694',
    default_options : [
        'warning_level=2',
    ],
)

max_num_up_buffers = get_option('max_num_up_buffers')
max_num_down_buffers = get_option('max_num_down_buffers')
buffer_size_up = get_option('buffer_size_up')
buffer_size_down = get_option('buffer_size_down')
printf_buffer_size = get_option('printf_buffer_size')
mode_default = '_'.join(['SEGGER_RTT_MODE', get_option('mode_default')])
memcpy_use_byteloop = get_option('memcpy_use_byteloop')
max_interrupt_priority = get_option('max_interrupt_priority')

conf_data = configuration_data()
conf_data.set('max_num_up_buffers', max_num_up_buffers)
conf_data.set('max_num_down_buffers', max_num_down_buffers)
conf_data.set('buffer_size_up', buffer_size_up)
conf_data.set('buffer_size_down', buffer_size_down)
conf_data.set('printf_buffer_size', printf_buffer_size)
conf_data.set('mode_default', mode_default)
conf_data.set10('memcpy_use_byteloop', memcpy_use_byteloop)
conf_data.set('max_interrupt_priority', max_interrupt_priority)

configure_file(
    input : 'SEGGER_RTT_Conf.h.in',
    output : '@BASENAME@',
    configuration : conf_data,
)

src = [
    'src/SEGGER_RTT_ASM_ARMv7M.S',
    'src/SEGGER_RTT_printf.c',
    'src/SEGGER_RTT.c',
]

inc = include_directories('include', '.', is_system : true)

segger_rtt_lib = static_library('segger-rtt', src,
    include_directories : inc,
    implicit_include_directories: false,
    pic: false,
)

segger_rtt_dep = declare_dependency(
    include_directories : inc,
    link_with : segger_rtt_lib,
)
