# packer
Creating a packer image to use with vagrant and virtualbox.
  * image contains Docker , Go , Ruby , Vim , TCPDump , HTop , Tree.
  * OS to be upto date with patches

ubuntu_simple.json
{
  "builders":[
    {
      "type": "virtualbox-iso",
      "guest_os_type": "Ubuntu_64",
      "iso_url": "file://${location_of_iso_image_on_machine}",
      "iso_checksum": "${checksum_of_iso}",
      "iso_checksum_type": "sha256",
			"output_directory": "${LOCATION}/ubuntu_simple",
			"vm_name": "ubuntu_simple",
			"disk_size": "20000",
			"headless": "false",
			"http_directory": "http",
			"boot_wait": "5s",
			"boot_command": [
				"<esc><wait>",
				"<esc><wait>",
				"<enter><wait>",
				"Welcome to packer",
				"<enter>"
			],
			"ssh_timeout": "10m",
			"ssh_username": "vagrant",
			"ssh_password": "vagrant",
			"shutdown_command": "sudo systemctl poweroff",
			"vboxmanage": [
				["modifyvm","{{.Name}}","--memory","1024"],
				["modifyvm","{{.Name}}","--cpus","2"]
			]
    }
	],
	"post-processors": [
		{
			"type": "vagrant",
			"compression_level": "9",
			"output": "some-location/simple-ubuntu.box"
		}
	]
}
